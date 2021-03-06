Programming Assignment 1
---------------------------

In this assignment, you will review an Android application that
contains potential security vulnerabilities and/or code abstractions
that do not exhibit secure abstraction design best practices.  You
will identify these issues and complete a multiple choice auto-graded
quiz on the coursera website.  You will then be asked to fix a few of
these problems in the code.

Security is a continuing evolving field that requires diligance on the
part of developers.  As part of this assignment, you will need to read
about 2 security flaws in the Android Firefox app and Facebook SDK.

http://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-1484

http://blog.parse.com/2012/04/10/discovering-a-major-security-hole-in-facebooks-android-sdk/

When evaluating the code, you should ensure that any data that is
being taken as input from a permission-protected resource is not
written to a location that could allow another app without that
permission to access it.

## INSTRUCTIONS FOR PART 1

For Part 1 there are three lines that create vulnerabilties that can
leak sensitive data or permissions and two lines that are examples of
poor security abstraction design that make it easy to do things
insecurely.  Please follow the directions below to setup the code base
that you will be performing a security review on. When you have
identified the flaws described below, submit your answers through the
auto-graded quiz for Part 1:

https://class.coursera.org/mobilecloudsecurity-001/quiz/start?quiz_id=339

For Part 2, described below, you will need to fix a subset of these
flaws and submit your fixes for peer grading.

Note: One of the vulnerabilities in this assignment is patched in
Android SDK Versions 4.1 and up.  If you think that means it doesn't
matter, you should know that there are still many Android devices 
running older versions of Android (see: http://developer.android.com/intl/zh-CN/about/dashboards/index.html).  
We therefore recommend that you create an AVD that is
using Android 4.0 (api 14) for this assignment. Also, please make
sure your AVD has SD card memory since this application relies heavily
on external storage.

Be warned that some AVD's using below SDK 4.0 have reported some unexpected
behavior.

The application you will be inspecting is called iRemember, which we
have adapted from the 2014 version of Prof. Porter's MOOC on "Programming Mobile
Applications with Android Handheld Systems".  This application allows
users to create a "story" that consists of a time, date, title, image,
audio recording, body text, tags, and location.  The app stores this
data in a database and allows yourself and other users to view them at
a later time.  Normally, this application would use a ContentProvider
to facilitate online database interactions, but for simplicity we have
re-written part of the application to use the SQLiteDatabase that is
hosted by your device, so you don't need an internet connection to run
the application.

In this directory you'll find the source code for the iRemember
application, as well as an apk called VulnCheck.apk.  Once you install
the iRemember app, you may also install VulnCheck.apk, which is a
"malware" program that demonstrates how a malicious application might
exploit the vulnerabilites present in iRemember.  If you do not know
how to install an apk on your (emulated) device, there are
instructions at the bottom of this file.  There are also instructions
on how to emulate GPS location information in an emulated device.

The main goal of this project is to get a taste of auditing real-world
code for security vulnerabilities.  To accurately identify the
problems in iRemember, we recommend you watch through the Module 2
videos, which cover the types of mistakes you should be looking out
for, as well as certain security patterns that should be used for best
practice.


To Import the Project into Eclipse:

1. Do a "git pull" to download the new assignment into your local git repo, or 
   go to:
   
https://github.com/juleswhite/mobilecloudsecurity-15.git
   
   And click "Download Zip" in the bottom right hand corner to download the latest
   assignments. Unzip them wherever you like. 
   
2. Open Eclipse, and do File->Import->Existing Android Code->Browse

3. Browse to where you downloaded this assignment's code and select ok. 

To Run the iRemember Application, right click on the project and select 
[Run As] -> [Android Application]

To install VulnCheck.apk:

1. Start your emulated device.

2. Open a command line or terminal. If you don't know how to do this,
   Google is your friend. It depends very much on which operating
   system you're using.

3. Try executing adb by typing "adb" and pressing Enter. If adb
   executes, it should show a help menu, and you can skip Step 4. If
   your terminal says something like "Executable not found," then
   you'll need to manually locate adb in Step 4.

4. The adb executable is located in the [android-sdks]/platform-tools
   directory. You should open a terminal in this directory in order to
   execute the adb executable. Again, if you don't know how to do
   this, Google is your friend. On any platform, the "cd" (change
   directory) command is usually useful.

5. Make sure adb recognizes your device. Type "adb devices -l" and
   press Enter. adb should list all the devices it is able to interact
   with, and you should see your AVD. If not, make sure that you
   actually started your AVD in step 1.

6. Use adb's install command to install the apk. Type "adb install
   $PATH_TO_APK", where $PATH_TO_APK is replaced by the path to
   VulnCheck.apk on your system. If everything goes well, adb should
   say something like "Success".

7. Start the application. On your AVD, go into the applications
   menu. You should see the application installed as
   "W7-A6-VulnCheck".

If you do not have any experience with the Android Debugger Bridge
(adb), we highly recommend reading up on it here:
	
http://www.vogella.com/tutorials/AndroidCommandLine/article.html
http://developer.android.com/tools/help/adb.html

To send GPS information to the AVD (from eclipse):

1. Start your emulated device

2. In eclipse, open the DDMS Perspective. (Window->Open Perspective->DDMS)

3. In the devices tab (which should be on the left), select your device by clicking on it.

4. Click on the emulator tab (which should be on the right). If the emulator tab is not there,
   open it by doing Window->Show View->Other->Android->Emulator Control

5. At the bottom of the emulator control tab, there should be a section called "Location Controls"
   Enter the location information you would like to send to the device, then click "Send"

If you are not using Eclipse (or you want to be really cool), you can
use the emulator console, documented here:

http://developer.android.com/tools/devices/emulator.html#console

The key command is "geo fix".

## INSTRUCTIONS FOR PART 2

In the second part of the assignment, you will need to fix two of the five
security issues. Those two issues are found in the following files:

. AndroidManifest.xml
. LoginActivity.java

Please modify these two files to fix the security issues in them.
When you have correctly modified the files to fix these issues, the
security vulnerability checker will no longer be able to record sound
or get login information from iRemember.  You should leave comments
describing what you fixed and why. 
