# Snoozy - Snoopy Screensaver for Android TV and Google TV

Snoopy now wants to sleep on your Android TV screen. Will you let him?

## Features

* Multiple Snoopy activites so you don't get bored
* Different backgrounds and foregrounds
* Auto night mode or you can pick light, dark or random.
* Enable and disable time (clock display)
* Preview screensaver
* No admob, no google analytics, no tracking, no crashlytics only the videos and the activity to display it

## Download

Check the [Releases page](https://github.com/theothernt/AerialViews/releases) there are two variants app-release.apk and app-release-1080.apk
The first file includes 720p videos so the file size is low and it should run smoothly on boxes that have low ram. If your box is a performance beast download the 1080 version and enjoy Snoozy in HD.

## How to set Snoozy as the default screensaver

If you click the open screensaver settings button in the app and it shows a panel where you can pick Snoozy as your screensaver then do that and stop reading.
If that doesn't work but you know what adb is run these commands

```
adb shell settings put secure screensaver_components com.overdevs.snoozy/.SnoozyDreamService
adb shell settings put secure screensaver_default_component com.overdevs.snoozy/.SnoozyDreamService
adb shell settings put secure screensaver_enabled 1
adb shell settings get system screen_off_timeout 300000
```
and your screensaver should show up after 5 minutes of the TV being idle. If you ever get bored how to remove the screensaver is at the bottom of this page.

If you didn't get any of that continue reading.

Since 2023, nearly all devices that ship with Google TV, running Android TV 12 or later, have no user-interface to change the screensaver to a 3rd party one...

* __Chromecast with Google TV, Google TV Streamer__
* __Recent MECOOL devices__
* __Recent TCL, Philips, and Sony TVs__
* __onn. Google TV devices (excluding the 2021 model)__
* __Fire TV (won't work with Fire OS 8.1 and above)__

But it can be done manually. Here is an overview of the steps...

1. Enable Developer mode, enable USB debugging, then find the IP address of your device
2. Use a Mac, iPhone, PC or Android phone with the required software or app
3. Connect to your Android/Google/Fire TV device
4. Run two ADB commands, one to set Snoozy as the default screensaver, the other to set how long it takes the screensaver to start

The full instructions are below, please click or tap to expand each step.

<details>
<summary>Enable Developer Mode on your Android/Google TV</summary>
&nbsp;

Navigate to the Settings menu on your device, then to the About screen. Depending on the device…

`Settings > System > About` or
`Settings > Device Preferences > About`

Scroll down to __Build__ and select __Build__ several times until you get the message "You are now a developer!"

Return to __Settings__ or __Settings > System__ and look for the newly enabled __Developer options__ page.

On the __Developer options__ page, look for the __USB debugging__ option and enable it.

Next, find the __IP address__ of your device. Try looking in the Network & Internet settings of the device, check the properties of the current LAN or WIFI connection - that should list the current IP address eg. 192.168.1.105
</details>

<details>
<summary>Enable Developer Mode on Fire Stick/TV</summary>
&nbsp;

Open __Settings__, then navigate to __My Fire TV__ then the __About__ screen.

Highlight your device name and press the action button on your remote seven times.

You'll now see a message confirming "You are now a developer", and it'll unlock the __Developer Options__ in the previous menu.

Navigate to the __Developer Options__ page, look for the __ADB debugging__ option and enable it.

Next, find the IP address of your device and make a note of it. Navigate to the __About__ then __Network__ screen, which will show your current IP address eg. 192.168.1.120
</details>

<details>
<summary>Allow Auto Launch on TCL TVs</summary>
&nbsp;

If you have a TCL TV with Google TV, you need to allow the Auto Launch permission so that Snoozy can be launched from the background when the screensaver starts.

Otherwise, the screensaver cannot be started, either automatically, or manually via the Screensaver menu shortcut, unless the Snoozy app has been recently opened.

1. Open the __Safety Guard__ app on your TV
2. Navigate to `Permission Shield > Auto Launch Permission`
3. Change the `Auto manager` at the top to `Closed` - this allows you to manually select which apps can auto-launch instead of the system deciding automatically
4. Scroll to __Snoozy__ and change it to `Opened`

Not all TCL TVs have the same software and features. If the above __Safety Guard__ app does not exist on your TV, the following ADB command might help…

Android TV v13 or less:
```sh
appops set com.overdevs.snoozy APP_AUTO_START allow
```

Android TV v14 or greater
```sh
appops set com.overdevs.snoozy AUTO_START allow
```

You can confirm the available options:
```sh
appops get com.overdevs.snoozy
```

</details>
<details>
<summary>Connect using atvTools (iOS or Android)</summary>
&nbsp;

[atvTools](https://play.google.com/store/apps/details?id=dev.vodik7.atvtools) is a free app available for both iPhone and Android that lets you run ADB shell commands against your Android TV directly from your phone — no PC required.

Once installed, make sure USB/Network debugging is enabled on your TV, then open atvTools and connect to your TV using its IP address. Navigate to the __Shell__ tab and tap the command input field. Run the following command to set Snoozy as the default screensaver:
```sh
settings put secure screensaver_components com.overdevs.snoozy/.SnoozyDreamService
```

Alternatively, atvTools has a dedicated __Screensaver__ button in the __Tools__ tab — however this only previews or triggers the current screensaver and does not let you change which app is used, so the shell command above is still required to point the system at Snoozy.

</details>


<details>
<summary>Connect using an iPhone</summary>
&nbsp;

Find an iPhone app that is capable of running ADB commands, [such as iSH Shell](https://ish.app/), which is free.

Once installed, run the app and install the Android Tools with the following commands…
```sh
apk update
apk add android-tools
```

To check if the ADB command is working, try typing…
```sh
adb version 
```

After pressing return, you should see something like this
```sh
Android Debug Bridge version 1.0.41
Version  31.0.0p1-android-tools
```

Now you can execute ADB commands.
</details>

<details>
<summary>Connect using an Android phone</summary>
&nbsp;

Find an Android app that is capable of running ADB commands, [such as Remote Termux](https://play.google.com/store/apps/details?id=com.termux), which is free.

Once installed, run the app and install the Android Tools with the following commands…
```sh
pkg update
pkg install android-tools
```

To check if the ADB command is working, try typing…
```sh
adb version 
```

After pressing return, you should see something like this
```sh
Android Debug Bridge version 1.0.41
Version  34.0.0p1-android-tools
```

Now you can execute ADB commands.
</details>

<details>
<summary>Connect using a Mac</summary>
&nbsp;

Download the official [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools) for Mac.

Extract the files from the ZIP archive to a folder. Then open a Terminal or Command Prompt and navigate to the folder.

To check if the ADB command is working, try typing…
```sh
adb version
```

After pressing return, you should see something like this
```sh
Android Debug Bridge version 1.0.41
Version  35.0.0-11411520
```

Now you can execute ADB commands.
</details>

<details>
<summary>Connect using a PC with Windows</summary>
&nbsp;

Download the official [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools) for Windows.

An alternate option is [Tiny ADB and Fastboot Tool (Portable version)](https://androidmtk.com/tiny-adb-and-fastboot-tool) but they both work in the same way.

Extract the files from the ZIP archive to a folder. Then open a Terminal or Command Prompt and navigate to the folder.

To check if the ADB command is working, try typing…
```sh
adb version
```

After pressing return, you should see something like this
```sh
Android Debug Bridge version 1.0.41
Version  35.0.0-11411520
```

Now you can execute ADB commands.
</details>

<details>
<summary>Extra steps for Chromecast with Google TV HD &amp; 4K</summary>

Since the update to Android TV 14, the Chromecast with Google TV (CCwGTV) has a bug which affects ADB. Normally, ADB uses port 5555 but on the CCwGTV the port is randomised.

This means the `adb connect <ip_address>` command will likely fail with a 'connection refused' message.

As a work-around, we can use the wireless debugging connection...

1. In `Settings > System > Developer options > Wireless debugging`, select Pair device with pairing code

2. Run the command: `adb pair <ip_address>:<port>`

3. The IP and port are displayed on the TV upon selecting Pair device with pairing code

4. ADB then asks for the pairing code displayed on the screen.

5. Once entered, you should see a message confirming that wireless debugging is connected.

You should be connected to your CCwGTV device with ADB. Now you can run `adb shell` and the other commands in the instructions that follow.

</details>

<details>
<summary>ADB command - set Snoozy as the default screensaver</summary>
&nbsp;

Connect to your Android TV device and start a command shell...
```sh
adb connect <ip_address>
```

:information_source: *Use the IP address of your device from earlier steps, it should be something like 192.168.1.98*
```sh
adb shell
```

:information_source: *The first time you connect to your Android TV device, you will probably see a confirmation dialogue asking to "allow" the connection*

Next, set Snoozy as the default screensaver with this command…
```sh
settings put secure screensaver_components com.overdevs.snoozy/.SnoozyDreamService
```

Optional: Confirm that the command was run successfully, as there is no confirmation when the command above is run.
```sh
settings get secure screensaver_components
```

If set correctly, you should see...
```sh
com.overdevs.snoozy/.SnoozyDreamService
```

</details>

<details>
<summary>ADB command - extra command for Fire TV + Fire OS 7.6.x.x</summary>
&nbsp;

Recent updates to Fire OS mean extra commands are required for Snoozy to function properly as the default screensaver.

Like with previous ADB commands, connect to your Android TV device and start a command shell. Then run the following commands...
```sh
settings put secure screensaver_default_component com.overdevs.snoozy/.SnoozyDreamService
settings put secure contextual_screen_off_timeout 300000 
settings put secure screensaver_enabled 1
```

</details>

<details>
<summary>ADB command - extra command for Fire TV + Fire OS 8.1.x.x</summary>
&nbsp;

Fire OS 8.x introduces a new Ambient Experience screensaver. This must also be disabled for Snoozy to run normally.

To disable the Ambient Experience, run this ADB command...
```sh
settings put secure amazon_ambient_enabled 0
```

Then reboot your Fire TV for the setting to take effect.

</details>

<details>
<summary>ADB command - change the screensaver timeout</summary>
&nbsp;

To change the default timeout use this command with a value in milliseconds. So, 5 minutes is 300000, 10 minutes is 600000 and so on.
```sh
settings put system screen_off_timeout 600000
```

:information_source: *On modern Google TV devices (Android TV 12+), the minimum value is 6 minutes or 360000. If you set a value lower than this, the screensaver won't start.*

</details>

<details>
<summary>How to revert back to the default screensaver</summary>
&nbsp;

If you would like to stop using Snoozy and revert back to the original screensaver, there are two options…

* Reset your device. Doing so will also reset the screensaver preference
* Use an ADB command to enable the default screensaver, depending on your device

1. Follow the instructions above to connect to your Android/Google TV device using an iPhone, Android phone, Mac, PC, etc
2. Run one of the following commands...

### To restore the default Google TV ambient screensaver
```sh
settings put secure screensaver_components com.google.android.apps.tv.dreamx/.service.Backdrop
```

### To restore the default Fire TV screensaver
```sh
settings put secure screensaver_components com.amazon.bueller.photos/.daydream.ScreenSaverService
```

### To restore the default (older) Android TV backdrop screensaver
```sh
settings put secure screensaver_components com.google.android.backdrop/.Backdrop
```

</details>
All these instructions were taken from https://github.com/theothernt/AerialViews/blob/master/README.md a great motivator for making my own screensaver app.
