Batch APK Tool 3.7.5 by Space Network

BATCH APKTOOL is a powerful shell that combines several tools for working with APK files.
Allows you to batch deodex, decompile, modify resources and smali-code, recompile, sign, align (zipalign) APK, ZIP, JAR-files.
Additionally, it is possible to connect plugins, view the source Java code of APK, JAR and DEX files, work with the device via ADB, etc.

Preparation for work:
Unpack the archive. In the path to the utility and in the names of the files to be processed, avoid long paths, the use of special characters (exclamation mark !, percentages%, carriages ^ etc.) and Russian letters.

1. Deodexation:
1.1 Place the entire contents of the /system folder of the firmware in the _system utility folder. You can download files directly from the device, see paragraph 3.4.
1.2 Specify the API Level (menu item [84]) corresponding to the Android version of the decoded firmware. If there is a build.prop file in the _system folder, the API level will be detected automatically.
1.3 Select the version of smali (menu item [83]) with which you will perform deodexation. smali-1.4.2 is only suitable for API level <= 17.
1.4 Select the menu item [01]. The files will be decoded directly in the _system folder. The contents of this folder are ready to be flashed into the device.
1.5 If there were symlinks in the firmware, they will be displayed at the end of the deodexation log.
1.6 To copy the decoded APKs or JAR files for further processing, select the menu item [02] or [03]. The files will be copied to the _INPUT_APK or _INPUT_JAR folders, respectively.

2. Decompilation and recompilation:
2.1 Place the files to be processed in the _INPUT_APK folder.
2.2 If you are parsing system files from firmware, place all APK files from the system/framework folder of that firmware in the _framework utility folder; otherwise, leave the folder _framework empty.
2.3 Select a menu item [1]. The disassembled applications appear in the _INPUT_APK folder.
2.4 Make the necessary changes.
2.5 If you parse system files, CLICK option [89] - this will save the original signature of the system APKs. If the option [89] is included, during the recompilation the application will be signed with the key selected in item [90].
2.6 Select [3]. Repackaged, signed (if enabled) and aligned APKs will be located in the _OUT_APK folder.

3.   ADB:
Allows you to work with the device through the Android Debug Bridge. For ADB to work correctly, you need:
On PC:
- Install the ADB driver for your device.
On your device:
- Enable settings for developers. To do this, go to Settings -> About phone, and several times click on the Build number item.
- In Settings - For developers, turn on the Debug Mode, and in the Superuser Mode item, select "For applications and ADB".
3.1 Item [10] - this is where you should start working with ADB. There are two possible connection options:
- USB - connect via USB and display connected devices. When you first connect, in the pop-up window on the device, you need to check the box "Always allow debugging from this computer".
- Wi-Fi - Wi-Fi connection. The mode requires a client, such as this https://play.google.com/store/apps/details?id=com.ttxapps.wifiadb
.2 Item [11] - Install the APK on the device.
3.3 Point [12] - request superuser rights for ADB and remount the /system folder for writing.
3.4 Item [13] - copying files from the corresponding folders on the phone to the folder _system utility.
3.5 Item [14] - copying files to the appropriate folders on the phone.
Sub-item [1] copies files directly through adb push, for this the /system folder must be mounted for writing through the point [12]. If item [12] cannot mount the /system folder for writing (error adbd cannot run as root in production builds, etc.), you need to use copying through subparagraph [2].
Subparagraph [2] uses an alternative copying method using the su binary (it is necessary to give superuser rights to the adb shell).
3.6 Item [15] - save the screenshot in the project folder (requires android 4.0 or higher).
3.7 Item [16] - record video from the screen and save it to the project folder (requires android 4.4 or higher).
3.8 Item [17] - the terminal of the device.
3.9 Item [18] - output the most important system logs (logcat (main, radio, events), dmesg and bugreport) and save them to a file in the project folder.
Subparagraph [6] is intended to save a table of inline-methods of flashing. This can help if the firmware is not decoded by the standard method (only for Android < 5.0).
3.10 Item [19] - various reboot options.
3.11 Item [20] - brief information about the android version and file system.
3.12 Point [21] - shuts down the ADB server correctly. With this command, you must shut down ADB, otherwise safely removing the device will not work.

4. Additional features:
4.1 Items [04], [05], [06] and [07] are intended for decompilation and recompilation of APK or JAR files using baksmali-smali. Only smali code is decompiled.
To do this, place the APK files in the _INPUT_APK folder (JAR files in the _INPUT_JAR folder), select the smali version, specify the API level, decompile, make the necessary changes and recompile.
Repackaged, signed (if the corresponding option is enabled) and aligned files will be located in the _OUT_APK folders (_OUT_JAR).
4.2 Item [4] allows you to sign APK, ZIP, JAR files. Place the files to be signed in the _INPUT_APK folder, and the signed and aligned files will be located in the _OUT_APK folder.
4.3 Option [5] allows you to align (zipalign) APK files. Place the files to be aligned in the _INPUT_APK folder, the aligned files will be located in the _OUT_APK folder.
4.4 Option [6] allows you to view the Java source code of the APK, JAR and DEX files, as well as the resources of the APK files.
4.5 Item [7] allows you to run plugins. If you want to create your own plugin, see the examples in the binplugins folder.
On Telegram Channel (https://t.me/SpaceBatch) plugins are available for cloning apks, optimizing the size of graphic files, patching protection by signature, etc.
4.6 Items in the MAINTENANCE category allow you to clear the corresponding folders of the utility.

5. Some more information:
5.1 The menu item [80] allows you to switch between projects. The name of the project corresponds to the name of the folder in which the work will be carried out. The default project name is ".", this corresponds to the root folder of the utility.
5.2 The menu items [81] and [82] allow you to select one file from the _INPUT_APK and _INPUT_JAR folders to be processed, respectively. By default, all files "*" are selected.
5.3 If one version of apktool reports an error during decompilation or recompilation, try another version (menu item [85]). Any version of apktool and smali can be added to the bin folder, and they must be named apktool_%versionnumber%.jar, smali-%versionnumber%.jar, and baksmali-%versionnumber%.jar.
5.4 When the option [86] is enabled, corrupted resources (if any) that lead to errors when decompiling the form "Invalid config flags detected. Dropping resources" will be stored in the res*-ERR* folders. You will have to fix them manually before recompiling.
5.5 With the option [87] enabled, the APK will be rebuilt in expert mode - the original APK will be taken as a basis for the build, and modified files will be added to it.
The mode can help in the case when the application assembled in the standard mode does not work (apktool incorrectly set the compression ratio, the application is sensitive to resource recompilation, etc.). Read more here http://4pda.ru/forum/index.php?showtopic=557858&view=findpost&p=58676347
NOTE: The mode is always enabled for apktool 1.x. It is possible to increase the size of the resulting APK.
5.6 The menu option [88] allows you to select the version of AAPT that is used when recompiling the APK, or auto-detection.
5.7 The [90] menu item allows you to select a key to sign APK, ZIP, and JAR files. You can add your own keys to the bin folder, they must be named %keyname%.pk8 and %keyname%.x509.pem
5.8 You can change the language of the utility interface by selecting the menu item [91]. If you want to add a translation into your language to the utility distribution, write to the utility's topic on the 4PDA forum: http://4pda.ru/forum/index.php?showtopic=557858
5.9 You can change the font size in the utility window by clicking PKM on the title bar of the utility window -> Properties -> Font.

6. Advanced settings (menu item [00]):
6.1 Items [1] and [2] allow you to select the utility by which the decoding will be performed. Read more here http://4pda.ru/forum/index.php?showtopic=557858&view=findpost&p=50674880
6.2 When enabling the [3] option, symlink files will be deleted after deodexation. The symlink code for updater-script is always stored at the end of the deodexation log.
6.3 Option [4] offers several options for saving the original AndroidManifest.xml when recompiling applications in standard mode. Read more here http://4pda.ru/forum/index.php?showtopic=557858&view=findpost&p=54594895
6.4 Decompilation with option [5] enabled will remove debug information (.local, .param, .line, etc.) from the smali code. Thanks to this, it becomes more convenient to compare smali files with each other (for example, from different versions of the same application).
6.5 When the option [6] is enabled, an additional decompilation prompt will be displayed if a folder with a decompiled application is detected.
6.6 When recompiling with the option [7] enabled, the serial number will be appended to the name of the output file, instead of overwriting.
6.7 To automatically open the work log when decompilation is complete, set the option [8] to YES mode. To prompt you to open the log after each operation, use the MANUAL mode.
6.8 When the option [9] is enabled, an audible notification will be issued at the end of decompilation/recompilation.



Thanks to the authors of the components used in BATCH APKTOOL:
- UnpackerFirmware plugin from unix3d
- 7-Zip  https://www.7-zip.org/
- Android SDK  https://developer.android.com/studio/index.html
- apktool  https://ibotpeaches.github.io/Apktool/
- BG  https://web.archive.org/web/20180926041545/http://consolesoft.com/p/bg/
- cecho  https://www.codeproject.com/Articles/17033/Add-Colors-to-Batch-Files
- ConX
- Foreign LINUX  https://github.com/wishstudio/flinux
- IniFile  http://www.horstmuc.de/wbat32.htm#inifile
- jadx  https://github.com/skylot/jadx
- Java  https://java.com
- Mtee  https://ritchielawrence.github.io/mtee/
- nhrt
- NirCmd  http://www.nirsoft.net/utils/nircmd.html
- SmaliEx  https://github.com/testwhat/SmaliEx
- Python  https://www.python.org/
- smali  https://github.com/JesusFreke/smali
- Strings  https://technet.microsoft.com/en-us/sysinternals/strings.aspx
- Swiss File Knife  http://stahlworks.com/dev/swiss-file-knife.html
- UnicodeEscape2UTF8  http://www.xinotes.net/notes/note/813/
- vdexExtractor  https://github.com/anestisb/vdexExtractor
- Wfile  http://www.horstmuc.de/w32dial.htm#wfile
- yq  https://github.com/mikefarah/yq
- Zip  http://www.info-zip.org/Zip.html

Special thanks to Batch ApkTool translators into other languages:
- Ukranian - Volodiimr and Dtuffg
- Türkçe - Hakan Güven
- Lietuvių - Shimas5
- Magyar - gidano

... as well as authors of other utilities, testers and users.


History of changes:
v3.7.5
- Updated apktool (2.5.1_20201211), smali (2.4.0_20200330), jadx (1.2.0-b1456), Python (3.7.9), Java (11.0.9).
- Added decoding of Android 9.0 - 10.0
- Updated UnpackerFirmware 1.7.0 RC plugin: added support for "Super partitions image".
- Updated plugin remove_classes_dex 1.5.1, UnicodeEscape2UTF8 v1.0.4.
- Signature now uses apksigner.jar: added support for APK Signature Scheme v2-v3.
- Added option to select AAPT version (AAPT1, AAPT2 or AUTO) in the settings.
- The option "Add a sequence number to the name of the output file, instead of overwriting" has been added to the advanced settings
- Removed luyten decompiler, I recommend the BytecodeViewer plugin to view the java code.
- Various bug fixes and improvements.

v3.7.4
- Updated apktool (2.4.1), smali (2.3.4), jadx (1.0.0-b1166), luyten 0.5.4 (procyon 0.5.36), dex2jar (2.1_20190905), Java (11.0.5), Python (3.7.5).
- All operations with JAR files now apply alignment. It can help if the firmware does not start after decoding or editing the JAR files.
- The Dalvik bytecode to JVM enjarify bytecode translator is replaced by dex2jar.
- Fixed some bugs.

v3.7.3
- Updated apktool (2.4.1_0303), smali (2.2.6), jadx (0.9.0-b656), vdexExtractor (0.5.3_1108), luyten 0.5.4 (procyon 0.5.33), Python (3.7.2), Java (8u201).
- Updated Turkish by Hakan Güven.
- Added Lithuanian language by Shimas5.
- Fixed several bugs.

v3.7.2
- Updated apktool (2.3.4_0702), smali (2.2.4_0711), oat2dex (0.90_0605), vdexExtractor (0.4.1_0610), jadx (0.7.2 build 474), UnpackerFirmware plugin (1.6.0), Python (3.6.6), adb, zipalign.
- In the advanced settings added the option to select a utility for decoding Android 8.x and above (baksmali or vdexExtractor).
- Many improvements to deodexation algorithms.
- Added Andycar remove_classes_dex plugin to remove classes.dex from APK/JAR files.
- Added Turkish by Hakan Güven.
- Fixed some bugs.

v3.7.1
- Updated apktool (2.3.4_0503), oat2dex (0.90_0420), jadx (0.7.2 build 429), UnpackerFirmware 1.4.4, Java (8u171).
- Faster display and saving of Logcat logs (about 3 times).
- Added saving log from the previous reboot (last).
- The option to select a utility for decoding Android 6.x-7.x has been added to the advanced settings again (oat2dex is faster than baksmali, but errors are possible).
- The option in the advanced settings "Save original AndroidManifest.xml" by default is now set to NO.
- Fixed some bugs.

v3.7.0
- Batch ApkTool is now 64-bit! For 32-bit Windows (and Windows XP) a separate version will be posted.
- Updated apktool (2.3.3_0413), jadx (0.7.2 build 427), oat2dex (0.90), python (3.6.5), adb, zipalign.
- Added decoding of Android 8.1 (using the utility vdexExtractor).
- Added UnpackerFirmware plugin from unix3d for unpacking firmware images (instead of the outdated SDATunpacker).
- All "CANCEL" items in the Batch ApkTool menu are now selected with the number 0.

v3.6.9
- Updated apktool (2.3.2), smali (2.2.3), enjarify (0329), jadx (0.7.2 build 413), Java (8u161).
- The option to enable experimental support for aapt2 has been added to the advanced settings (only for apktool 2.3.2 and above).
- Fixed some bugs.

v3.6.8
- Updated apktool (2.3.1), smali (2.2.2), Java (8u151).
- Added display of time spent on decompilation/recompilation.
- Fixed detection of Java 9 version.
- Apktool 1.5.2 has been removed from the distribution.

v3.6.7
- Updated apktool (2.2.5_0827), sdat2img (2017-28-08), Java (8u144).
- Added checking for the presence of files necessary for work.
- Fixed minor bugs.

v3.6.6
- Updated apktool (2.2.3), smali (2.2.1), luyten 0.5.3, sdat2img (2017-01-04), Java (8u131).
- Added Android O decoding.
- Removed the ability to decode Android 6 and above via oat2dex.

v3.6.5
- Updated enjarify (0301).
- The standard Windows dialog is now used to select files.
- The options "Save the original AndroidManifest.xml", "Warn about overwriting the folder during decompilation" and "Sound alerts" have been added to the advanced settings.
- Added output of messages to the tray.
- Fixed hovering of logs display on the logs screen.

v3.6.4
- Updated apktool (2.2.2), smali (2.2_0108), enjarify (0122), luyten 0.5.0 (procyon 0.5.32), sdat2img (2016-11-23), Java (8u121).
- The FindFramework plugin has been added to the distribution.
- Fixed extracting files with the same name, but in a different register, from sqsh archives during deodexation.

v3.6.3
- Updated apktool (2.2.2_1023), smali (2.2_1024).
- Added support for API Level 25 (Android 7.1 Nougat Preview).
- Fixed the signature of some APK files.

v3.6.2
- Updated apktool (2.2.1), smali (2.2_1018), enjarify (0928), sdat2img (0924), Java (8u111).
- Added an alternative way to copy files to the /system folder (item [14->2], the su binary is used).
- Added the ability to selectively install the APK from the _OUT_APK folder.
- Now baksmali is used by default for decoding Android 6 and above (you can enable oat2dex in the advanced settings [00]).
- Added file count when decoding via baksmali.
- Improvements and bug fixes.

v3.6.1
- Updated apktool (2.2.1_0819), enjarify (0831), luyten 0.4.9 (procyon 0.5.32), SDATunpacker plugin (1.0.1).
- Optimized API level >= 23 decoding algorithm via baksmali.
- Added support for decoding odex*.sqsh files.
- Significantly accelerated and improved the simlink search algorithm (simlinks are supported after unpacking images by Rom Helper).
- Added the option to enable/disable the removal of symlinks after deodexation (in advanced settings).

v3.6.0
- Updated apktool (2.2.0), luyten 0.4.8 (procyon 0.5.32), Java (8u101).
- Added _system folder for firmware decoding.
- Added automatic detection of API Level if there is a build.prop file in the _system folder.
- The deodexation log has been moved to a separate file log_deodex.txt
- Symlink files are now deleted after deodexation (symlink code for updater-script is saved at the end of the deodexation log).
- Accelerated recompilation in expert mode with a large number of changes in the decompiled file.
- SDATunpacker plugin has been added to the distribution.
- Removed old versions of oat2dex.
- Various improvements and bug fixes.

v3.5.0
- Updated apktool (2.2.0_0621), smali (2.2_WIP_0529).
- Various improvements to the deodexation algorithm.
- Added advanced settings (menu item [00]) with the ability to select the API level >= 23 deodexation method.
- Plugins can now use the Python 3 interpreter to work.
- The Dalvik bytecode to JVM dex2jar bytecode translator is replaced by enjarify.

v3.4.5
- Updated apktool (2.1.1), smali (2.1.2_0424), oat2dex (0.87_0426), luyten 0.4.7 (procyon 0.5.32), Java (8u91).
- Changed the decoding method of Android 6.0.
- CopyBack plugin has been added to the distribution.

v3.4.4
- Updated apktool (2.1.0), oat2dex (0.86_0316), Java (8u77).
- Added Decoding of Android N.
- Boot.oat deodexation error no longer interrupts the deodexation process.

v3.4.3
- Updated apktool (2.1.0_0229), oat2dex (0.86_0226), smali (2.1.2_0228), Java (8u73).
- Added copying of /system/app, /system/priv-app, /system/framework folders from the device to the utility folders (p. 13-> 4).
- Fixed processing of some files with non-standard zip-headers (when decoding and building in expert mode).
- Updated adb, zipalign binaries.

v3.4.2
- Updated apktool (2.1.0_0106), oat2dex (0.86_0107), smali (2.1.1), luyten 0.4.6 (procyon 0.5.32).
- Accelerated decoding of Android 6.0 files.
- Fixed deodexation of files with multiple classes.dex (Android 6.0).
- Added copying files from _OUT_APK to /system/framework.
- Added Ukrainian language (thanks volodiimr).

v3.4.1
- Updated apktool (2.0.3_1024), smali (2.1.0_1018), oat2dex (0.85_1013), jadx (0.6.1 build 221), Java (8u65).

v3.4.0
- Added decoding of Android 6.0
- Updated apktool (2.0.2_0930_), smali (2.1.0_1002), oat2dex (0.83_0930), jadx (0.6.1 build 220).

v3.3.4
- Updated apktool (2.0.2_0912_fix), jadx (0.6.1 build 218).

v3.3.3
- Updated apktool (2.0.2_0821), smali (2.0.7_0906), oat2dex (0.83_0909), luyten 0.4.4 (procyon 0.5.30), jadx (0.6.1 build 215), Java (8u60).
- Updated adb binaries.
- Fixed reading hidden symbolic links.

v3.3.2
- Added decoding of .odex.gz files.
- Fixed the signature of zip files for recovery.
- Minor fixes.
- Updated apktool (2.0.2_0811), jadx (0.6.1 build 210), oat2dex (0.83_0806).

v3.3.1
- Added decoding of .apk files in the _framework folder.
- The function of copying files to the device (point 14) now copies files recursively along with subdirectories.
- Added copying decoded APKs and JAR files to _INPUT_APK and _INPUT_JAR folders.
- Updated apktool (2.0.1), jadx (0.6.1 build 206), Java (8u51).

v3.3.0
- Added Spanish, Chinese, German, Turkish and French.
- Changed the logic of deodexation of files: now files are decoded directly in the _app, _priv-app and _framework folders.
- Improved deodexation algorithms: files of all architectures are now decoded in one pass.
- Deodexation log added output of symbolic links (for updater-script).
- Fixed deodexation of files with multiple classes.dex.
- Updated apktool (2.0.1_0629), smali (2.0.7_0619), jadx (0.6.1 build 203), oat2dex (0.83).

v3.2.1
- Added Belarusian language
- Logs are now saved in UTF-8 with BOM
- Increased java heap size for oat2dex.jar

v3.2.0
- Added support for localization files. Russian and English languages have been added to the distribution.
- Added initial plugin support. The functions of replacing resources without recompiling and converting unicode sequences to UTF-8 have been transferred to plugins.
- Added plugin to customize the color of the main interface elements.
- The jd-gui java source code decompiler has been replaced by luyten 0.4.4 (procyon 0.5.28).
- Added output of color formatted text in logcat. Logs are now saved in real time during browsing.
- Fixed ignoring changes in the libs folder.
- Updated apktool (2.0.1_0524), smali (2.0.6_0523), jadx (0.6.1 build 198), oat2dex (0.81).
- Various improvements and bug fixes.

v3.0.1
- Added a counter of processed files.
- Frames are now installed from the _framework folder and all its subfolders.
- Updated apktool (2.0.0), smali (2.0.5_0410), jadx (0.6.0), jd-gui (1.0.0-RC4), dex2jar (2.0).
- Updated Java 8u45 (in the standalone version of BAT).

v3.0
- Improved the algorithm of the expert mode.
- Added decoding of x86 architecture applications (Android 5.0).
- Added saving of the table of inline-methods of flashing (paragraph 18->8) (see readme p. 3.10).
- Increased decompilation rate.
- Updated apktool (2.0.0-RC4_0322), smali (2.0.5_0321), jadx (0.5.5 build 181), signapk.

v2.9.9
- Fixed the recompilation function if an aapt file is present in the C:Windows folder.exe
- Updated jadx (0.5.5 build 171).

v2.9.8
- Improved Java detection
- apktool 2.x now uses external aapt.
- Updated apktool (2.0.0 RC4), jadx (0.5.5 build 166).

v2.9.7
- Added expert mode for APK build (see readme p. 5.5).
- Added error logging for [6 Zipalign files].
- Improved the function of decompiling applications on systems where the system VARIABLE PATH is incorrectly set
- Updated jadx (0.5.5 build 165).

v2.9.6
- Items 04-07 now decompile all dex files, not just classes.dex.
- Updated apktool (2.0.0 rc3 from 21.01.2015), smali (2.0.5), jadx (0.5.5 build 164).
- Updated Java 8u31 (in the standalone version of BAT).

v2.9.5
- Fixed ignoring changes made to assets and lib folders when using apktool 1.x (the defect appeared in BAT289)
- Returned compatibility with beta versions of apktool 2.x

v2.9.4
- Added decoding of *.odex.xz files in the _framework folder
- Code optimization

v2.9.3
- Added decoding of *.odex.xz files (Android 5.0)
- Updated jadx (0.5.5 build 163).

v2.9.2
- Added the ability to decode Android 5.0 applications
- Fixed incorrect decompilation of applications, if the file names of their smali-code contained invalid characters
- Updated jadx (0.5.5 build 162).

v2.9.1
- Improved deodexation function.
- Updated apktool (2.0.0 rc3 from 30.12.2014), smali (2.0.3 from 29.12.2014), jadx (0.5.5 build 157).
- Updated aapt.exe for apktool 1.5.2

v2.9
- Added information about the versions of the components used to the logs.
- Frames when using apktool_2.x are now installed in the utility folder.
- Updated apktool (2.0.0 rc3 from 26.12.2014), jadx (0.5.5 build 155).

v2.8.9
- Fixed saving application version and SDK version changed via apktool.yml.
- Updated apktool (2.0.0 rc2 from 02.11.2014), smali (2.0.3 from 06.11.2014), jd-gui (0.3.7 RC1), jadx (0.5.5 build 142).

v2.8.8
- Returned creating a backup in the _backup folder.
- The Standalone version of Batch ApkTool now uses Java 8.
- Updated apktool (2.0.0 rc2 from 20.10.2014), jadx (0.5.3 build 131).
- Improvements and bug fixes.

v2.8.7
- When copying files to system folders, they are now set to 644 rights
- Updated APK build algorithm via apktool 2.x
- Logs are now opened in the editor associated with txt files in the system
- Updated apktool (2.0.0 rc2 from 05.10.2014), jadx (0.5.3 build 128).

v2.8.6
- Added detection of Java version when running the utility
- Updated aapt.exe for apktool 1.5.2
- Updated apktool (2.0.0 rc1 from 24.09.2014), jadx (0.5.3 build 126).

v2.8.5
- Slightly increased the rate of deodexation and recompilation (by about 10-20%)
- Added option [87 Don't write out debug info]
- Added the ability to select a key to sign APK, ZIP and JAR files
- Updated apktool (2.0.0 rc1 from 27.08.2014), smali (2.0.3 from 28.08.2014), jadx (0.5.3 build 120).

v2.8.4
- Added support for apks containing multiple dex files
- Updated apktool (2.0.0 rc1 from 16.08.2014), jadx (0.5.2).

v2.8.3
- Fixed the situation in some users when after decompilation the folder of the disassembled application was empty
- Updated jadx (0.5.2 build 102).

v2.8.2
- Added operations of batch installation of applications (including to SD card) and copying files to the device
- Forbidden to run multiple copies of the utility
- Changed the method of displaying colored text (for utility translators into Russian and other languages)
- Updated jadx (0.5.2 build 96).

v2.8.1
- Added a couple of checks when running the utility
- Added item [20 info] - information about android version and file system
- Updated smali (2.0.3 from 22.07.2014), jadx (0.5.2 build 92).

v2.8
- Added copying (pull) folders /system/app, /system/priv-app and /system/framework from the device
- Added the ability to save the full bugreport of the device (logs > bugreport)
- The format of line endings in log and bug report files is now standard for Windows - CR+LF
- Updated jadx (0.5.2 build 88)

v2.7.1
- Significantly accelerated conversion of unicode escapes to UTF-8
- Now parsing through [06 Decompile JARs (only smali)] does not use the -l and -s parameters.
- Updated jadx (0.5.1 build 82).

v2.7
- Added conversion of unicode escapes to UTF-8 (smali).
- Added colors)
- Optimized the algorithm for detecting the changes made, increased the speed of recompilation (up to 2 times)
- Added smali-baksmali version 1.4.2.
- Updated aapt, adb and zipalign binaries.
- Updated jadx (0.5.1 build 80).
- Fixed incorrect date in the name of logs and screenshots, if the format of regional standards is different from Russian.

v2.6
- Increased the speed of recompilation (depending on the source file and the changes made - up to 3 times)
- Changing the logic of opening the log, again)): two modes - MANUAL and ON.
- Updated apktool (2.0.0 rc1 from 2014.06.18), jadx (0.5.1 build 78).

v2.5
- Added [86 Keep broken resources] option to force decompilation of corrupted resources.
- Added writing files to the /system/priv-app folder.
- Now, after each operation, a suggestion to open a log is displayed.
- Updated apktool (2.0.0 rc1 from 25.05.2014), jadx (0.5.1 build 70).

v2.4.1
- Reverted to the old algorithm for determining changes in AndroidManifest.xml, without taking into account apktool.yml.
- Fixed a crash when working with files containing brackets in the name (), as well as when entering some special characters instead of the menu item number.
- Updated jadx (0.5.1 build 68).

v2.4
- Added the ability to select one file for processing.
- Updated apktool (2.0.0 rc1), jadx (0.5.1 build 63).
- Fixed saving changes to apktool.yml.
- Minor improvements and bug fixes.

v2.3
- Added the ability to connect ADB via Wi-Fi.
- Fixed video recording by command [17].
- Updated adb and aapt binaries.
- Minor improvements.

v2.2
- Added viewing of Java source code APK, JAR and DEX files.
- Added video recording from the screen via ADB (requires android 4.4 or higher).
- Changed the logic of the menu items [11], [13], [14] and [15].
- Fixed a recompilation bug using apktool 1.x that appeared in v2.1.

v2.1
- Added the ability to create and upload projects.
- The recompilation and assembly points of the resulting APK are combined into one item.
- The signature option has become global and now applies to all output APKs.
- Signature option enabled by default
- The smali code when parsed through smali now matches the smali code when parsed through apktool.
- Executable files of the program are moved to the bin folder

v2.0
- First) version

Author - Space Network (Batch by BurSoft)
@SpaceNetworkEU
