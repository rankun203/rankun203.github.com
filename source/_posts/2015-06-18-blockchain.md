---
title: Bitcoin playground
date: 2015-06-18 18:52:09
categories:
- programming
tags:
- Bitcoin
- BlockChain
- Coinbase
- php
---

## 使用 Blockchain 的服务进行比特币交易

## Use blockchain bitcoin service to transfer bitcoins

### [Wallet api](https://blockchain.info/api/blockchain_wallet_api)

```
https://blockchain.info/merchant/$guid/payment
?password=$main_password
&second_password=$second_password
&to=$address
&amount=$amount
&from=$from
&fee=$fee
&note=$note
```

Request tips:

> The My Wallet API provides a simple interface Merchants can use interact with their wallet. Blockchain.info will decrypt the wallet on our server manipulate it as necessary and re-save. HTTP GET and POST are supported. However, if a POST request is sent without "Content-Type: application/x-www-form-urlencoded" header, some endpoints may not work correctly.

<!-- more -->

### /payment

```
https://blockchain.info/merchant/59fee004-0115-4861-8e4a-7f8af3ba31fb/payment
?password=$main_password
&second_password=$second_password
&to=$address
&amount=$amount
&from=$from
&fee=$fee
&note=$note
```

returns:

```
{
  "error": "Api Access is disabled. Enable it in Account Settings."
}
```

Then we have to enable API access from the Account Settings on Blockchain.

```
[Account Settings] -> [IP Restrictions] -> [Enable Api Access]
```

Then we call the API, returns:

```
{
  "error": "API Access approval needed. Please check your email."
}
```

From our Email inbox, we got a alert `Authorize API access attempt`, we only have to click the link to get the access continue.

Otherwise, user can add the server ip to their account IP white list.

> From the 1st December 2014, in order to use this API, access must be explicitly enabled, and all client ip addresses whitelisted by the wallet owner. Manage access in [Account Settings] -> [IP Restrictions]. Wallets created via the Create Wallet API can bypass this by including the same API key used to create the wallet, in all requests.

Then we update our request to this form(filled some blank parameters):

```
https://blockchain.info/merchant/a4bde787-3512-4b68-a669-91771dff514c/payment
?password=password
&second_password=password
&to=1NV6sH3hS2u5Fnbey5Vh32ho3P3x23CXM2
&amount=1
&from=123m1f3ZeWV5RMfJgrPNb3t3rvVbeB5mTD
&fee=1
&note=This is only for testing.
```

Of course, got an 'error':

```
{
  "error": "No free outputs to spend"
}
```

That's it!

### Transfer real bitcoins

Next, charge a few bitcoins to my wallet, then transfer 100฿ to another wallet.

API call finished, returns:

```
{
  tx_hash: "7f2c5f0c108351370779824db23e01628240f423b1490ec48c52a7654555afee",
  message: "Sent To Multiple Recipients"
}
```

### Transfer process seems to be failed

But the target wallet **didn't** get the money.

Check the Blockchain dashboard, it shows:

> Unconfirmed Transaction!

Thus, I need to **confirm** this transaction.

For the exactly meaning of **confirm**, I checked the transaction I transfered from LocalBitcoins to Blockchain, it shows `7 Confirmations`. So I think it's some kind of p2p server confirmation. Maybe not managed by myself.

After over 20 minutes, it still not confirmed.

### Transfer some bitcoins to another account again

In the meantime, I did it again, to a different wallet(at Coinbase, 200 bit):

```
{
  error: "Insufficient Funds Available: 0 Needed: 10200"
}
```

YES, That's because my previous transaction was still unconfirmed.

As a note, php script here:

```php
<?php
/**
 * DEBUG: XDEBUG_SESSION_START=docker_php
 */

$guid = "guid-identifier";
$firstpassword = "password";
$secondpassword = "second_password";
$amounta = "200";
$to = "1NV6sH3hS2u5Fnbey5Vh32ho3P3x23CXM2";
$recipients =
    urlencode('{
                  "' . $to . '": ' . $amounta . '
               }');

$json_url = "https://blockchain.info/merchant/$guid/sendmany?password=$firstpassword&second_password=$secondpassword&recipients=$recipients";

$json_data = file_get_contents($json_url);

$json_feed = json_decode($json_data);

$message = $json_feed->message;
$error = $json_feed->error;
$txid = $json_feed->tx_hash;

echo json_encode($json_feed);
```

### Bitcoins transfer was succeeded a hour ago

Finally, after a couple of hours, I noticed the message there: *+68 minutes to confirm*, That means the transfer finally succeeded.

```
06/18/2015 19:17	0.000002	 	1E6Ki2WdWzDKng35hohQmmuTG1yfnMd3QF
```

**Too slow to me**, I blamed this on the influence of LocalBitcoins™, too small to be noticed ;p
