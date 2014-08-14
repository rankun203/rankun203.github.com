---
layout: post
title: "Android Activity之间传递数据"
date: 2013-09-27 16:22
comments: true
categories: [java, android]
---
Android在Activity间传递数据的方法有以下几种
------------------------------------------
###使用Intent绑定内容
-  在一个类里面调用[`intent.putExtra(tagString, ctn)`][putStringExtra]存入数据。
-  在启动后的[Activity][Activity]里面调用传进来的intent的[`intent.getStringExtra(tagString)`][getStringExtra]方法来获取数据（存什么类型就用什么类型获取）。
    -  在另一个[Activity][Activity]里面使用[`getIntent()`][getIntent]来获取当前的[Intent][Intent]。

###使用全局变量[`Application`][Application]
-  创建一个Java类`MyApp`, 继承自[`android.app.Application`][Application]
-  在[`AndroidManifest.xml`][AndroidManifest.xml]里面指定[`application`][mainfest-application]的[`android:name`][mainfest-application-name]的值为刚刚创建的类

这样无论在程序的什么地方用[`getApplication()`][getApplication]方法拿到的[Application][Application]对象都是`MyApp`的实例（*准确的说是Application的实例，但明显就是一个MyApp，当然可以转成MyApp*）。

如果在MyApp里面定义一些变量，再定义一些`getter`和`setter`，就可以在任何地方读取或设置这些全局变量。
####示例代码
#####`AndroidManifest.xml`
```xml
<application
android:name="org.rankun.learn_intentapplication.MyApp">
...
<activity>
...
</activity>
</application>

```
#####`MyApp.java`
```java
public class MyApp extends Application {
		public String attr;
		//...
}
```
#####`SomeActivity.java`
```java
MyApp myApp = (MyApp)getApplication();
myApp.xxx();
```
<!--more-->
###使用剪切板[`ClipboardManager`][ClipboardManager]
- 在任意方法中使用[`getSystemService(Context.CLIPBOARD_SERVICE)`][getSystemService]获得[`ClipboardManager`][ClipboardManager]，然后调用其[`setPrimaryClip(ClipData clip)`][setPrimaryClip]方法设置剪贴板的内容。
    - 参数[`ClipData`][ClipData]可以通过`ClipData`的静态方法`ClipData.newPlainText("tag", "string")`进行设置。
- 在想读取的地方拿到[`ClipboardManager`][ClipboardManager]后，调用`clipboardManager.getPrimaryClip().getItemAt(0).coerceToText(this).toString()`就可以拿到剪贴板的内容。

####示例代码
#####`OneActivity.java`
```java
String msg = "I'm 20.";
ClipboardManager clipboardManager = (ClipboardManager)getSystemService(Context.CLIPBOARD_SERVICE);
clipboardManager.setPrimaryClip(ClipData.newPlainText("msg", msg));
```
#####`AnotherActivity.java`
```java
ClipboardManager clipboardManager = (ClipboardManager)getSystemService(Context.CLIPBOARD_SERVICE);
String str = clipboardManager.getPrimaryClip().getItemAt(0).coerceToText(this).toString();
```
###获取Activity的返回值
- 在当前[Activity][Activity]中使用[`startActivityForResult()`][startActivityForResult]启动一个Activity，并添加一个[`onActivityResult()`][onActivityResult]方法来接收返回的数据。
    - 在启动新的Activity时，传入的[Intent][Intent]对象里面可以包含一些关于这次询问的信息，requestCode在自定义的[`onActivityResult()`][onActivityResult]方法中作为变量requestCode回传，这样，如果我们启动了多个ActivityForResult，就可以通过requestCode判断是哪一个ActivityForResult返回了。
- 在被调用的[Activity][Activity]中使用[`getIntent()`][getIntent]来获取启动这个[Activity][Activity]的[Intent][Intent]，该[Intent][Intent]应该包含了调用者传递过来的一些[putExtra信息][putStringExtra]。
- 被调用的[Activity][Activity]在处理好结果准备返回。
    - 创建一个用来返回的[Intent][Intent]
	- 将要返回的数据[putExtra][putStringExtra]在这个Intent中
	- 调用当前Activity的[`setResult()`][setResult]方法设置resultCode和用来返回的Intent
	- 调用当前Activity的[`finish()`][finish]方法结束本Activity的生命周期，结果将会被返回到调用这个Activity的Activity
- 主调Activity的[`onActivityResult`][onActivityResult]方法触发之后，需要的数据已经包含在传入的Intent中
    - 可以通过判断requestCode来确定是哪一个ActivityForResult返回了
	- > resultCode	The result code to propagate back to the originating activity, often RESULT_CANCELED or RESULT_OK
	- 可以从Intent对象中获取返回的数据

####示例代码
#####`MainActivity.java`
```java
//例如可以用某个按钮的onClick事件触发这个方法运行
public void queryRes(View view) {
	EditText et1 = (EditText) findViewById(R.id.et1);
	String qesString = et1.getText().toString();
	Intent other = new Intent(this, OtherActivity.class);
	other.putExtra("qes", qesString);
	startActivityForResult(other, 5);
}
```
<div style="text-align:center;font-size:40px;">↓</div>
#####`OtherActivity.java`
```java
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.other);

	//解析传来的数据
	Intent requestIntent = getIntent();
	String qes = requestIntent.getStringExtra("qes");
	((TextView)findViewById(R.id.qes)).setText(qes);
}

//例如可以用某个按钮的onClick事件触发这个方法运行
public void procAndRtn(View view) {
	String ansString = ((EditText)findViewById(R.id.otheractivity_et_1)).getText().toString();
	Intent rtnIntent = new Intent(this, MainActivity.class);
	rtnIntent.putExtra("ans", ansString);
	setResult(RESULT_OK, rtnIntent);
	finish();
}
```
<div style="text-align:center;font-size:40px;">↓</div>
#####`MainActivity.java`
```java
//5, 6, data
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	super.onActivityResult(requestCode, resultCode, data);
	if(resultCode == RESULT_OK) {
		if(requestCode == 5) {
			String ans = data.getStringExtra("ans");
			TextView tv = (TextView)findViewById(R.id.main_activity_ans_tv);
			tv.setText(ans);
		}
	}
}
```
[startActivityForResult]: https://developer.android.com/reference/android/app/Activity.html#startActivityForResult(android.content.Intent,%20int) 
[onActivityResult]: https://developer.android.com/reference/android/app/Activity.html#onActivityResult(int,%20int,%20android.content.Intent)
[Intent]: https://developer.android.com/intl/zh-cn/reference/android/content/Intent.html
[putStringExtra]: https://developer.android.com/reference/android/content/Intent.html#putExtra(java.lang.String,%20java.lang.String[])
[getStringExtra]: https://developer.android.com/reference/android/content/Intent.html#getStringExtra(java.lang.String)
[Activity]: https://developer.android.com/intl/zh-cn/reference/android/app/Activity.html
[getIntent]: https://developer.android.com/reference/android/app/Activity.html#getIntent()
[Application]: https://developer.android.com/intl/zh-cn/reference/android/app/Application.html
[AndroidManifest.xml]: https://developer.android.com/intl/zh-cn/guide/topics/manifest/manifest-intro.html
[mainfest-application]: https://developer.android.com/guide/topics/manifest/application-element.html
[mainfest-application-name]: https://developer.android.com/intl/zh-cn/guide/topics/manifest/application-element.html#nm
[getApplication]: https://developer.android.com/reference/android/app/Service.html#getApplication()
[ClipboardManager]: https://developer.android.com/intl/zh-cn/reference/android/content/ClipboardManager.html
[getSystemService]: https://developer.android.com/reference/android/content/Context.html#getSystemService(java.lang.String)
[setPrimaryClip]: https://developer.android.com/reference/android/content/ClipboardManager.html#setPrimaryClip(android.content.ClipData)
[ClipData]: https://developer.android.com/intl/zh-cn/reference/android/content/ClipData.html
[setResult]: https://developer.android.com/reference/android/app/Activity.html#setResult(int)
[finish]: https://developer.android.com/intl/zh-cn/reference/android/app/Activity.html#finish()
