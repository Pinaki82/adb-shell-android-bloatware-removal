# Delete Bloatware and Install Apps on Android via Android Debug Bridge (ADB)

Do you need the ADB shell to install apps on your phone when anyone can easily check the option to 'allow installation from unknown sources' and use the phone browser to download APK files? The short answer is, Yes.

The Reason:

Google accounts enrolled in Google's Advanced Protection Program have limited choices of app installation from different sources due to security reasons. On the other hand, some people prefer libre and open source applications for security. Open source projects are usually secure due to the nature of their publicly auditable source code. F-Droid is a repository that hosts such Android applications. Apps on F-Droid are compiled from the source code on their server, so those apps are secure. Here's the catch. Google won't allow users of Advanced Protection Program enrolled accounts to install any other app store on their devices. The phones of those users won't have any effect on having the button 'allow installation from unknown sources' checked either. Here comes another question. Will F-Droid be able to install apps on those phones even though F-Droid can be installed from the PC using the ADB shell? No. Possibly, F-Droid won't be allowed to update apps that are also available on both the app stores (Google Play Store). However, F-Droid is a treasure of information to know alternative open-source applications. Find an app on F-Droid, then search for it on Play Store. The ADB shell will be the last resort to get an app on the phone after downloading the app from F-Droid's repository, only if it's unavailable in Google Play Store.

'I'm not impressed. My Google account is not enrolled in Advanced Protection Program. Do I really need the ADB shell anyway? ' Yes. In case you want to get rid of sticky bloatware supplied by the phone vendor. Those sticky apps are irremovable. The regular uninstallation method won't do the trick.

Thus, knowing to use the ADB shell is a plus.

What you need:

1. A computer. It can be a Windows or a Linux computer.

2. An Android device (phone/tablet/Android-powered eReader etc.).

3. 15 minutes of patience.

Ref:

Google: how to sideload apps using the adb

https://www.lifewire.com/how-to-sideload-android-apps-4689188

Google: uninstall apps from the adb shell

https://www.droidwin.com/remove-uninstall-bloatware-apps-from-android-via-adb-commands/

> Fun Factor: Turning on USB Debugging is not Jailbreaking. You aren't going to Root your phone. (^_^)

**If you are looking for a tutorial to root your phone, you should look somewhere else.**

I never suggest people to ROOT their phones. It's a clear threat to security.

## Part 1:

#### Windows:

Download the ADB from Google:
 https://dl.google.com/android/repository/platform-tools-latest-windows.zip

Unpack the zip archive with 7-Zip (*use only 7Z).

##### Registry Patch:

You'll need a registry patch so that you can open the Windows command prompt inside a folder from a simple Right-Click context menu.

Filename:

```
TerminalHere.reg
```

```
Windows Registry Editor Version 5.00

; Open CMD Here
; 'Open Terminal Here' MS equivalent

; https://github.com/microsoft/terminal/issues/1060
; https://stackoverflow.com/questions/27632612/comment-in-reg-file
; https://docs.microsoft.com/en-us/previous-versions/windows/embedded/gg469889(v=winembedded.80)?redirectedfrom=MSDN

[HKEY_CURRENT_USER\Software\Classes\Directory\Background\shell\Open CMD Here\command]
@="C:\\Windows\\system32\\cmd.exe"
```

#### *-Ubuntu:

```
sudo apt install android-tools-adb
```

The two core aspects of installing/uninstalling apps from the ADB shell:

1. Developer Mode.
2. USB Debugging.

## Part 2:

#### On the phone:

**Settings App** -> **About Phone** -> **MIUI Version** -> **Tap 7 Times**

You'll get a warning that looks like, 'You're 4 steps away from putting your phone into developer mode', after three consecutive taps.

> You're 4 steps away from putting your phone into developer mode

Ref: https://www.getdroidtips.com/enable-option-usb-debugging-redmi-4-4x/

Google: toggle developer mode redmi 4

**NOTE:** Connect your device to the internet. Otherwise, Xiaomi Corporation Inc. won't let you turn on USB Debugging.

![ADB-devel-0001](https://user-images.githubusercontent.com/16861933/153182956-93326aa7-108a-49c9-8f84-1ee0f00548ce.jpg)

Turn on USB Debugging from the Developer Options.

**Settings App** -> **System Settings** -> **Additional Settings** -> **Developer Options** -> **DEBUGGING** -> **USB Debugging**, **Install via USB**, & **Verify apps installed over the USB**.

![ADB-devel-0002](https://user-images.githubusercontent.com/16861933/153183217-f282a105-1aa4-40b1-a96d-ececa0a6fd49.jpg)

![ADB-devel-0003](https://user-images.githubusercontent.com/16861933/153183308-e605979d-5f37-45cd-a9d9-4c1290ac053d.jpg)

![ADB-devel-0004](https://user-images.githubusercontent.com/16861933/153183370-537ec2f5-77a4-42d1-a77a-9c61721c35bb.jpg)

![ADB-devel-0005](https://user-images.githubusercontent.com/16861933/153183421-11e04519-8e2e-43d1-ade0-3ab4b553a8a6.jpg)

![ADB-devel-0006](https://user-images.githubusercontent.com/16861933/153183488-4fda7c93-861e-4a26-b6de-3c5143f5e413.jpg)

## Part 3:

PC Side:

Right-click inside the extracted folder 'platform-tools_rxx.x.x-windows\platform-tools' and choose to open a command prompt window there.

#### CMD:

```
O:\platform-tools_r32.0.0-windows\platform-tools>ls
AdbWinApi.dll     adb.exe          fastboot.exe         make_f2fs.exe           mke2fs.exe         systrace
AdbWinUsbApi.dll  dmtracedump.exe  hprof-conv.exe       make_f2fs_casefold.exe  source.properties
NOTICE.txt        etc1tool.exe     libwinpthread-1.dll  mke2fs.conf             sqlite3.exe
```

The `ls` command worked on my PC because I have MSYS2 installed on my system. And also, MSYS2 'bin' directories are added to the system path on my system.

```
C:\msys64\usr\bin
C:\msys64\usr\x86_64-pc-msys\bin
C:\msys64
C:\msys64\mingw64\bin
C:\msys64\opt\node-v14.17.6-win-x64
```

Not everyone needs MSYS2. So, for now, stick to the more common Windows command: `dir`.

## Part 4:

#### The Next Step

```
adb devices
```

Allow USB Debugging from the phone. Or else, you'll see that the connected device is unauthorised, and you won't be able to install/uninstall anything on your phone from your PC's terminal.
See the outputs below:

```
O:\platform-tools_r32.0.0-windows\platform-tools>adb devices
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
xxxyyywwwzzz    unauthorized
```

```
O:\platform-tools_r32.0.0-windows\platform-tools>adb install "C:\Users\YourUserName\Downloads\F-Droid.apk"
Performing Streamed Install
adb: failed to install F-Droid.apk: Failure [INSTALL_FAILED_USER_RESTRICTED: Install canceled by user]
```

After authorising USB Debugging from the phone, the output will look something like this:

```
O:\platform-tools_r32.0.0-windows\platform-tools>adb devices
List of devices attached
xxxyyywwwzzz    device
```

## Part 5:

> NOTE: Don't ever install APK files downloaded from anywhere other than the F-Droid's repository. Any other third-party app stores are also not beyond scepticism. Even Google Play Store is a mixed bag. There is no shortage of malicious apps found on Google's own app store. Play Store comes preinstalled, so it is deemed secure by android users.

## App Installation:

Now you can install any app from the terminal. **Important:** Be sure to authorise the installation from the PC to the phone on the phone side. You'll see that a dialogue box appears on your phone asking your permission to allow the connected PC to perform the installation.

Examples:

```
adb install Your_app.apk
```

```
adb install F-Droid.apk
```

```
adb install "C:\Users\YourUserName\Downloads\F-Droid.apk"
```

If everything goes well, you'll be greeted with the 'success' message.

```
Performing Streamed Install...
Success
```

Example:

```
O:\platform-tools_r32.0.0-windows\platform-tools>adb install "C:\Users\YourUserName\Downloads\F-Droid.apk"
Performing Streamed Install
Success
```

## Part 6:

## App Uninstallation:

```
adb shell
```

Know the packages installed on your phone.

```
adb shell cmd package list packages -s
```

Take a backup:

```
adb shell cmd package list packages -s > "%USERPROFILE%\Documents\SystemApps.txt"
```

For older versions of Android:

```
pm list packages -s
```

Here's the output I received.

Depending on the phone and the apps installed on your phone, you may see something else. I try new applications and sometimes uninstall apps I don't need. So, the list may grow or shrink in the future. That's not something to be considered permanent. However, the output below will give us an overview of what it looks like from the ADB Shell.

```
package:com.miui.screenrecorder
package:com.android.cts.priv.ctsshim
package:com.google.android.youtube
package:com.qualcomm.qti.auth.sampleextauthservice
package:com.google.android.ext.services
package:com.android.providers.telephony
package:com.miui.powerkeeper
package:com.xiaomi.miplay_client
package:com.google.android.googlequicksearchbox
package:com.miui.fm
package:com.android.providers.calendar
package:com.android.providers.media
package:com.milink.service
package:com.qti.service.colorservice
package:com.google.android.onetimeinitializer
package:com.google.android.ext.shared
package:com.xiaomi.powerchecker
package:com.xiaomi.account
package:com.qualcomm.shutdownlistner
package:com.android.wallpapercropper
package:com.quicinc.cne.CNEService
package:com.xiaomi.mi_connect_service
package:com.xiaomi.micloud.sdk
package:com.wt.secret_code_manager
package:org.simalliance.openmobileapi.service
package:com.android.updater
package:com.android.documentsui
package:com.android.externalstorage
package:com.qualcomm.uimremoteclient
package:com.android.htmlviewer
package:com.qualcomm.svi
package:com.miui.securityadd
package:com.miui.gallery
package:com.android.mms.service
package:com.miui.msa.global
package:com.android.providers.downloads
package:com.qualcomm.qti.auth.sampleauthenticatorservice
package:com.xiaomi.payment
package:com.miui.securitycenter
package:android.autoinstalls.config.Xiaomi.santoni
package:com.qualcomm.qti.telephonyservice
package:com.miui.videoplayer
package:com.qualcomm.qti.auth.fidocryptoservice
package:com.google.android.configupdater
package:com.android.soundrecorder
package:com.miui.userguide
package:com.android.defcontainer
package:com.miui.guardprovider
package:com.android.providers.downloads.ui
package:com.android.vending
package:com.android.pacprocessor
package:com.qualcomm.cabl
package:com.miui.backup
package:com.xiaomi.mirecycle
package:com.miui.notification
package:com.miui.micloudsync
package:com.miui.daemon
package:com.android.certinstaller
package:com.android.carrierconfig
package:com.google.android.marvin.talkback
package:com.qti.qualcomm.datastatusnotification
package:android
package:com.android.contacts
package:com.qualcomm.wfd.service
package:com.miui.hybrid
package:com.miui.vsimcore
package:com.mi.webkit.core
package:com.miui.securitycore
package:com.android.egg
package:com.android.mms
package:com.android.mtp
package:com.android.stk
package:com.android.backupconfirm
package:com.xiaomi.simactivate.service
package:com.miui.player
package:com.miui.miservice
package:com.android.provision
package:org.codeaurora.ims
package:com.android.statementservice
package:com.google.android.gm
package:com.miui.sysopt
package:com.miui.system
package:com.google.android.apps.tachyon
package:com.android.calendar
package:com.miui.global.packageinstaller
package:com.miui.translation.kingsoft
package:com.miui.compass
package:com.qualcomm.qti.auth.secureextauthservice
package:com.google.android.setupwizard
package:com.miui.rom
package:com.qualcomm.qcrilmsgtunnel
package:com.android.providers.settings
package:com.android.sharedstoragebackup
package:com.mediatek.batterywarning
package:com.facebook.services
package:com.xiaomi.location.fused
package:com.google.android.music
package:com.android.printspooler
package:com.android.dreams.basic
package:com.android.incallui
package:com.fido.xiaomi.uafclient
package:com.android.frameworks.telresources
package:com.miui.bugreport
package:com.android.inputdevices
package:com.fido.asm
package:com.qualcomm.qti.auth.securesampleauthservice
package:com.qualcomm.qti.CdmaCallOptions
package:com.qualcomm.qti.StatsPollManager
package:com.qti.dpmserviceapp
package:com.android.fileexplorer
package:com.qti.xdivert
package:com.google.android.apps.docs
package:com.google.android.apps.maps
package:com.miui.translation.youdao
package:com.miui.cloudbackup
package:com.android.cellbroadcastreceiver
package:com.google.android.webview
package:com.android.server.telecom
package:com.google.android.syncadapters.contacts
package:com.android.keychain
package:com.android.camera
package:com.android.chrome
package:com.xiaomi.glgm
package:com.xiaomi.upnp
package:com.xiaomi.xmsf
package:com.google.android.packageinstaller
package:com.google.android.gms
package:com.google.android.gsf
package:com.google.android.tts
package:com.android.calllogbackup
package:com.miui.freeform
package:com.google.android.partnersetup
package:com.fingerprints.serviceext
package:com.google.android.videos
package:org.codeaurora.btmultisim
package:com.xiaomi.mipicks
package:com.dsi.ant.server
package:com.xiaomi.finddevice
package:com.android.proxyhandler
package:com.xiaomi.joyose
package:com.mi.android.globalFileexplorer
package:com.miui.notes
package:com.miui.wmsvc
package:com.xiaomi.misettings
package:com.google.android.feedback
package:com.google.android.printservice.recommendation
package:com.xiaomi.midrop
package:com.google.android.apps.photos
package:com.miui.translationservice
package:com.google.android.syncadapters.calendar
package:com.miui.cloudservice
package:com.android.managedprovisioning
package:com.miui.hybrid.accessory
package:com.android.dreams.phototable
package:com.miui.translation.xmcloud
package:com.miui.touchassistant
package:com.xiaomi.providers.appindex
package:com.android.providers.partnerbookmarks
package:com.google.android.gsf.login
package:com.android.smspush
package:com.mediatek.factorymode
package:com.mi.android.globalminusscreen
package:com.miui.calculator
package:com.android.wallpaper.livepicker
package:com.mi.AutoTest
package:com.miui.cloudservice.sysbase
package:com.miui.miwallpaper
package:com.facebook.system
package:com.xiaomi.bluetooth
package:com.qualcomm.qti.telephony.vodafonepack
package:com.google.android.backuptransport
package:com.miui.cleanmaster
package:com.android.storagemanager
package:com.miui.analytics
package:com.android.bookmarkprovider
package:com.android.settings
package:com.qualcomm.qti.ims
package:com.miui.weather2
package:com.quicinc.wbcserviceapp
package:com.qualcomm.location
package:com.xiaomi.scanner
package:com.android.cts.ctsshim
package:com.qualcomm.qti.tetherservice
package:com.miui.yellowpage
package:com.miui.antispam
package:com.qualcomm.qti.services.secureui
package:com.android.vpndialogs
package:com.android.email
package:com.wt.version_query
package:com.android.phone
package:com.android.shell
package:com.android.wallpaperbackup
package:com.android.providers.blockednumber
package:com.android.providers.userdictionary
package:com.android.emergency
package:com.qualcomm.qti.RIDL
package:com.android.location.fused
package:com.android.deskclock
package:com.android.systemui
package:com.android.bluetoothmidiservice
package:com.mi.globallayout
package:com.facebook.appmanager
package:com.xiaomi.discover
package:com.mi.dlabs.vr
package:com.miui.smsextra
package:com.android.thememanager
package:com.mipay.wallet.id
package:com.mipay.wallet.in
package:com.qualcomm.fastdormancy
package:com.qualcomm.qti.auth.fidosuiservice
package:com.miui.fmservice
package:com.android.thememanager.module
package:com.lbe.security.miui
package:com.android.bluetooth
package:com.qualcomm.timeservice
package:com.qualcomm.embms
package:com.android.providers.contacts
package:com.stability.camerastability
package:com.android.captiveportallogin
package:com.miui.core
package:com.miui.home
package:com.google.android.inputmethod.latin
package:com.miui.audioeffect
santoni:/ $
```

### Uninstall apps:

> NOTE: Do not uninstall any system app or essential app. Always double-check the app's purpose before removing an app. Try [this one](https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer&hl=en) to know the APK names of the apps installed on your phone.

Examples...

Google Pay (Tez) uses the UPI Payment Gateway, and it serves my purpose. I don't feel the need for any similar apps. Let me show you how I uninstalled the 'Mi Pay' app.

```
santoni:/ $ pm uninstall -k --user 0 com.mipay.wallet.in
Success
santoni:/ $ pm uninstall -k --user 0 com.mipay.wallet.id
Success
santoni:/ $
```

I also uninstalled the following apps. In some cases, I downloaded alternative apps, and in other cases, I don't see any reason for using some of the default apps. Privacy concerns had also been considered at the time of uninstalling some packages.

_Google Movies and TV:_

```
pm uninstall -k --user 0 com.google.android.videos
```

_Google Music:_

```
pm uninstall -k --user 0 com.google.android.music
```

_Android Mail Client:_ The default Android Mail Client App. It doesn't integrate well with some email clients. On top of that, this modified version is issued by Xiaomi Corporation. The issuer country shown was not the country I live in.

```
pm uninstall -k --user 0 com.android.email
```

_MIUI Video Player:_ I'll show you how to download VLC from F-Droid's repository and install the same using the ADB shell.

```
pm uninstall -k --user 0 com.miui.videoplayer
```

_MIUI Audio Player:_ I'll go for VLC.

```
pm uninstall -k --user 0 com.miui.player
```

_Android Notes:_ A modified version of the Android Notes App, created by Xiaomi. The app can't export files to TXT format and doesn't open files with the TXT extension. Other text files with different extensions are unsupported as well. The app also has a tendency to sync notes to Xiaomi's cloud services. No thanks! I have so many decent note-taking/to-do management/code-editor apps.

```
pm uninstall -k --user 0 com.miui.notes
```

_Google Photos:_ Google imposed storage limitations on their Google Photos service in 2021. The app occupied a lot of space on my phone's internal memory. I'd rather use the web interface when needed.

```
pm uninstall -k --user 0 com.google.android.apps.photos
```

_ShareMe - Xiaomi's File-Sharing app:_ Nobody's interested in downloading that Xiaomi app to send files to other devices unless they own a Xiaomi device. Most people ask for turning on the BlueTooth, and I also noticed transferring files from USB drives is the fastest possible way to go. Wireless file sharing apps have a reputation of not being suckless. Carry a 16GB thumb drive with two USB-A to Phone OTG adapters if you're in dire need. If wireless file transfer is your best bet, you may try Goggle's 'Files' app as well.

```
pm uninstall -k --user 0 com.xiaomi.midrop
```

_Xiaomi's Theme Manager:_ I use a minimalist launcher. Themes and notifications are not my cups of tea, and they are seemingly distracting. People need to detoxify their digital life. Computers were designed to help us to be more productive, not to make us lazy and infuriate us with distracting notifications from social media, news, advertisements, and bundled resource hog sluggish bloatware applications, which in turn make us counterproductive. I'm not a fan of Eye-Popping Themes and a whole bunch of distracting notifications for diverting my attention to somewhere else.

```
pm uninstall -k --user 0 com.android.thememanager
```

_Google Duo:_ Who uses Google's Duo? I'll go for Jitsi.

```
pm uninstall -k --user 0 com.google.android.apps.tachyon
```

_RedMi Calender:_ Another critical, however, modified default app by Xiaomi. It syncs my data to overseas servers, their cloud services. I use a different calendar app.

```
pm uninstall -k --user 0 com.android.calendar
```

_RedMi Gallery:_ I have a better Gallery app.

NOTE: After uninstalling the default Xiaomi Gallery app, I faced problems while grabbing screenshots. I had to re-install the gallery app. I'll show you how to re-install accidentally removed apps later.

```
pm uninstall -k --user 0 com.miui.gallery
```

I uninstalled Wallpaper Carousel also.

```
Success
```

### Get a list of all applications installed by you [[Ref](https://stackoverflow.com/questions/53634246/android-get-all-installed-packages-using-adb)]:

```
adb shell cmd package list packages -3
```

Save the result to a text file if needed:

```
adb shell cmd package list packages -3 > "%USERPROFILE%\Documents\UserInstalledApps.txt"
```

When done:

```
santoni:/ $ exit
```

Then,

Type, `exit`.

```
O:\platform-tools_r32.0.0-windows\platform-tools>exit
```

---

# IMPORTANT:

## If you have unintentionally uninstalled an app:

Ref:

https://forum.xda-developers.com/t/how-to-install-get-back-uninstalled-apps-apks-with-adb.3894235/

https://forum.xda-developers.com/t/how-to-install-get-back-uninstalled-apps-apks-with-adb.3894235/page-4#post-84291287

DuckDuckGo: adb shell Unknown command: install-existing

```
O:\platform-tools_r32.0.0-windows\platform-tools>adb shell
santoni:/ $ pm enable --user 0 com.miui.gallery
Package com.miui.gallery new state: enabled
santoni:/ $ pm dump com.miui.gallery | grep path
        path: /system/priv-app/MiuiGallery/MiuiGallery.apk
santoni:/ $ pm install -r --user 0 /system/priv-app/MiuiGallery/MiuiGallery.apk
Success
santoni:/ $
```

##### One-by-one:

Run the ADB Shell from the Windows CMD.

```
adb shell
```

In the ADB Shell, type...

```
pm enable --user 0 com.miui.gallery
```

...to re-enable the removed package.

Know the path to that app:

```
pm dump com.miui.gallery | grep path
```

Copy the path to the clipboard ('Click-n-drag + Enter' on Windows).

For example, `/system/priv-app/MiuiGallery/MiuiGallery.apk` or `/system/priv-app/FMRadio/FMRadio.apk`.

Then, paste the copied path at the end of the following character string:

```
pm install -r --user 0 
```

That is,

```
pm install -r --user 0 /system/priv-app/MiuiGallery/MiuiGallery.apk
```

Also notice that the command `adb shell cmd package install-existing com.miui.gallery` will return an error: `Unknown command: install-existing`

Therefore, it's best to stick to `pm install -r --user 0 /system/priv-app/APK_with_PATH`.

---

## Part 7:

Time to install a few more apps. Test what you've learned.

```
adb install "C:\Users\YourUserName\Downloads\F-Droid.apk"
adb install "C:\Users\YourUserName\Downloads\com.mkulesh.micromath.plus_319.apk"
adb install "C:\Users\YourUserName\Downloads\com.blacksquircle.ui_10007.apk"
adb install "C:\Users\YourUserName\Downloads\org.videolan.vlc_13040307.apk"
adb install "C:\Users\YourUserName\Downloads\org.koreader.launcher.fdroid_8849.apk"
adb install "C:\Users\YourUserName\Downloads\com.concept1tech.instalate_13.apk"
adb install "C:\Users\YourUserName\Downloads\com.foobnix.pro.pdf.reader_4334.apk"
```

KoReader is not available in Google Play. It's possibly the best all-rounder eBook reader out there on the android market. It takes a few hours to get accustomed to using the reader. Nevertheless, you'll get all the bells & whistles to manipulate eBooks on a tiny phone display. When you get everything to handle every facet of document files, you'll read much more comfortably on your phone, even if your phone has a relatively smaller display, like 4.7" or 5".

KoReader was designed for eReaders. The interface looks very different from the more traditional android applications' approach to the material design UI because their main focus is creating the best possible eBook reader app for eReader devices. It comes with an integrated dictionary. Stardict dictionary files can be added to extend the dictionary database further. External dictionary applications like GoldenDict can also be accessed. Pan and pinch zoom is not available, though. Instead, it has a different approach to zoom documents. It takes time to get used to with KoReader, but in the end, no other eBook Reader app feels even remotely close to this eBook reader application.

Librera PRO is another excellent eBook Reader for Android. It supports external dictionary applications, even WordWeb. Documents can be pinch zoomed and panned.

Cool Reader is also a good eBook Reader. It doesn't support static documents (PDF, DJVU etc.) which is a downside. External dictionary applications like GoldenDict are supported. Pan and pinch zoom is unavailable since EPUB, CHM, TXT, MOBI files are 'Reflowable Documents'. The text part in reflowable documents adapts to the screen properties. Images are scaled. Thus, ebooks in those formats are resized according to the screen size and resolution. However, Cool Reader allows users to change the font size.

---

---

## Part 8:

### Disable USB Debugging and Developer Mode:

1. Uncheck the following options:
- Install via USB.

- USB Debugging.
2. Revoke USB Debugging Authorisations.

![ADB-devel-0007](https://user-images.githubusercontent.com/16861933/153183665-06cf668c-b301-4a1c-b3e1-b33cc67461d0.jpg)

Press OK on the phone when prompted.

3. Disable Developer Options.

**Long Tap** on the **Settings** app -> **App Info** -> **Force Stop** & **Clear All Data**.

![ADB-devel-0008](https://user-images.githubusercontent.com/16861933/153183730-025d6d7b-c470-419d-8265-b16c186ca5c7.jpg)

![ADB-devel-0009](https://user-images.githubusercontent.com/16861933/153183762-2808126d-0671-4c4d-8bcf-af62fd74a2c7.jpg)

_Repeat_ it.

Go to the 'App Info' section of the required app (e.g., F-Droid) and allow network and storage permissions.

Reboot your PC and delete the folder 'platform-tools_rxx.x.x-windows' if you do not plan to use the ADB shell again.

## Part 9:

### How will you update the apps you installed using the ADB Shell?

#### ONE: For general users:

Check the option 'Unknown Sources', 'Allow Installation of apps from unknown sources. Now you're ready to update apps from F-Droid, as you update from Google Play Store. If, for any reason, you cannot update apps directly from the phone, try the ADB Shell again. Update the apps as you'd install apps using the same commands.

For example:

```
adb install "C:\Users\YourUserName\Downloads\org.koreader.launcher.fdroid_8849.apk"
```

Adding the `-r` option at the start will reinstall the app. I strongly advise you against doing so because if you reinstall an app, you're most likely going to lose its configuration files and settings.

In case you don't want to update apps from your PC, you can try updating the apps from F-Droid after turning on the option 'Unknown Sources'. It's much comfier to update apps from the phone.

#### TWO: For account holders of Google's Advanced Protection Program:

Turning on the option 'Unknown Sources' won't have any effect here.

The ADB Shell is always your best friend. Use the ADB Shell and update the apps from your PC's terminal.

---

===

Link to this document's repository: https://github.com/Pinaki82/adb-shell-android-bloatware-removal.git

You may wish to download the PDF or the EPUB version from the release section.

Recommended EPUB Viewer on Android (for smaller files) is [Cool Reader](https://play.google.com/store/apps/details?id=org.coolreader&hl=en). On the PC, try [Okular](https://okular.kde.org/). It's a multiplatform, multiformat document viewer by [KDE](https://kde.org/). Okular can open EPUB files. Windows and Linux both are covered.

To create the EPUB, I used [Sigil](https://sigil-ebook.com/).

The _README.md_ file, which is the main file to this guide, has been created with [Mark Text](https://marktext.app/). Also, the PDF version of the document was exported from [Mark Text](https://marktext.app/). Download **Mark Text** from [here](https://github.com/marktext/marktext). You can download the HTML version, but without an active internet connection, you won't see the screenshots.

===
