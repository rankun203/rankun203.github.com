title: Webpage screenshot has been automatically removed!
date: 2016-01-15 21:36:43
categories:
- chrome
tags:
- chrome
- plugin
---

### UPDATE (2016-02-10):

I've found there is still a record in `~/Library/Application\ Support/Google/Chrome/Default/Preferences` and deleted it, see if it works.

----

For those of you who suffering from the malicious Chrome plug-in called `Webpage screenshot` always saying it's removed automatically...

### Try this:

```bash
# Fire a commandline up, and go to your Chrome directory
cd ~/Library/Application\ Support/Google/Chrome

# Searching for it
find . -iname 'Webpage Screenshot'

# find out the directory and remove it, in my case:
cd Default/Extensions
rm -rf ckibcdccnfeookdmbahgiakhnjcddpki
```

If it does the job, then congrats, if not, post your idea below :)

Ideas come to my mind:

- `grep -r 'Webpage Screenshot' .`
- `grep -r 'ckibcdccnfeookdmbahgiakhnjcddpki' .`
