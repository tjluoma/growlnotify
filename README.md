growlnotify
===========

A shell script 'wrapper' for the actual [growlnotify][1] command.

## Requirements

* the actual [growlnotify][1] binary which is assumed to be installed at /usr/local/bin/growlnotify.

* Mountain Lion - because it uses `pgrep` and the one from `brew` isn't compatible with the one Apple included in 10.8. (Although this could easily be worked around, I'm only using 10.8 these days.)

* [Growl.app][2]. Obviously.

## Purpose

This script is intended to be placed in your $PATH before `/usr/local/bin/` so that this script will be called whenever you refer to `growlnotify`. This script will call the actual `growlnotify` but will do several other things as well.

1.	It will check to make sure that `growlnotify` is actually installed at `/usr/local/bin` and if it isn't, it will download and install it for you.

2. 	It will check to make sure that Growl.app is installed, and if it isn't, it will open the Mac App Store.app to the [Growl.app page][2] and wait for you to install it.

3. 	If Growl.app is installed and `growlnotify` is installed, it will check to make sure that Growl.app is running, and if it isn't, it will launch it. Don't want to auto-launch Growl when you log in to your Mac? No problem. Now it will start when needed (at least for your shell scripts).

4. 	Last but not least, this script will check to make sure that the `growlnotify` binary exits properly, and if it doesn't, it will kill Growl.app, restart it, and tries to send the `growlnotify` message again (because if `growlnotify` doesn't exit properly, it usually means that Growl.app is not responding properly). It will try 5 times, if it doesn't work after 5 times, it just gives up.

## Usage ###

Simply download and install this script as `growlnotify` somewhere other than /usr/local/bin/ and make sure that it occurs before /usr/local/bin/ in your `$PATH`. 

You could rename the actual `growlnotify` to something like `growlnotify.orig` and then install this to `/usr/local/bin/growlnotify` and then just change this line in the script:

	GN='/usr/local/bin/growlnotify'

to
	GN='/usr/local/bin/growlnotify.orig'

but that is not recommended because if you ever run this on a Mac which doesn't have the actual `growlnotify` installed, the installer will overwrite this script.

## "Why not just use Mountain Lion's notifications?"

Because they suck. Growl is 100% better than Mountain Lion's notifications. They're more customizable, they're able to show longer messages, and more apps support it.

[1]: http://growl.info/downloads
[2]: http://itunes.apple.com/us/app/growl/id467939042?mt=12
