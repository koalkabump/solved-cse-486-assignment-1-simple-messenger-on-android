Download Link: https://assignmentchef.com/product/solved-cse-486-assignment-1-simple-messenger-on-android
<br>
In this assignment, you will write a simple messenger app on Android. The goal of this app is simple: enabling two Android devices to send messages to each other. The purpose of this assignment is to help you see if you have the right background for this course. ​If you can finish this all by yourself without getting any help from others​, then it is probably the case that you have the right background. Please see for yourself!

There are four high-level challenges in this assignment:

<ul>

 <li>There will be a lot of reading involved in this assignment.​ This is because you need to read many tutorials/articles online.</li>

 <li>There will be a lot of infrastructure setup.​ This involves installing various software components and configuring them.</li>

 <li>There will be many trials and errors to make Android do what you want to do.​ This is true not just for Android but also for any platform/framework. Luckily, Android provides excellent official documentation. You will need to get used to reading the official developer website.</li>

 <li>There are networking restrictions that the Android emulator environment imposes. You​ need to get used to it for the assignment.</li>

</ul>

So here we go!

<h1>Step 1: Getting Started</h1>

<ul>

 <li>Unless you are already familiar with Android programming, the first thing you want to do is to follow the ​<u><a href="https://developer.android.com/training/index.html">tutorials</a></u>​.

  <ul>

   <li>It’s good to follow all the tutorials, but it’s not mandatory for this assignment.</li>

  </ul></li>

</ul>

However, please do follow the ones mentioned below.

<ul>

 <li>Please follow the first tutorial ​<u><a href="https://developer.android.com/training/basics/firstapp/index.html">“Building Your First App”</a></u>​ which will guide you through the process of installing necessary software and creating a simple app.

  <ul>

   <li>Important Note 1: ​Please use Android Studio. ​Eclipse is not supported any more.</li>

  </ul></li>

</ul>

○    Important Note 2: ​We use API 19 for this semester.

○    Important Note 2: ​Please make sure you use Java 8 or lower. Java 9 does not seem to play nicely.

○    Important Note 4​: There is one part of this tutorial where it instructs you to create an Android emulator instance (or AVD, Android Virtual Device). When you do it, it

will ask you to choose a system image.

■    Please make sure that you choose 19 for the API level, x86 for the ABI, and Android 4.4 (Google APIs) for the target.

■    Please also make sure that you enable VM acceleration. Please read <u>​</u><u><a href="https://developer.android.com/studio/run/emulator-acceleration.html#accel-vm">this</a></u> for instructions. x86 system images with VM acceleration run a lot faster with less resources, so it’s going to be easier to run on your laptop. For this to work, you will need to have a machine that supports VT-x or equivalent.

○    If you’re using a 64-bit version of Ubuntu, you might have to install some additional packages. Please refer to <u>​</u><u><a href="https://stackoverflow.com/questions/27078052/android-studio-build-error-on-ubuntu-install">this</a></u><u>​</u><a href="https://stackoverflow.com/questions/27078052/android-studio-build-error-on-ubuntu-install">.</a>

<ul>

 <li>Please follow the fourth tutorial <u>​</u><u><a href="https://developer.android.com/training/basics/activity-lifecycle/index.html">“Managing the Activity Lifecycle”</a></u><u>​</u> which will give you some basic concepts to understand the code given (as described in Step 2 below).</li>

 <li>Please also follow the tutorial ​<u><a href="https://developer.android.com/training/basics/data-storage/index.html">“Saving Data”</a></u>​ which you will need from PA2. But this is not necessary for this PA.</li>

 <li>For more information on Android programming, please refer to the following pages.

  <ul>

   <li><u><a href="https://developer.android.com/guide/components/fundamentals.html">Application Fundamentals</a></u></li>

  </ul></li>

</ul>

○    <u><a href="https://developer.android.com/guide/components/activities.html">Activities</a></u>

○    <u><a href="https://developer.android.com/guide/components/processes-and-threads.html">Processes and Threads</a></u>

<ul>

 <li>For the success of all the programming assignments, it is critical​ that you know how to use the Android emulator and debug your app because you will spend lots of time using the emulator and debugging. The following pages will give you the information on debugging.

  <ul>

   <li><u><a href="https://developer.android.com/tools/devices/emulator.html">Using the Android Emulator</a></u></li>

  </ul></li>

</ul>

○     <u><a href="https://developer.android.com/tools/debugging/index.html">Debugging</a></u><u>​</u><a href="https://developer.android.com/tools/debugging/index.html">,</a> especially <u>​</u><u><a href="https://developer.android.com/tools/debugging/debugging-studio.html">with Android Studio</a></u> <u>​</u>​<u><a href="https://developer.android.com/tools/debugging/debugging-log.html">using the Log class</a></u>​.

<h1>Step 2: Setting up a Testing Environment</h1>

You will need to run two AVDs in order to test your app. Unfortunately, Android does not provide a flexible networking environment for AVDs, so there are some hurdles to jump over in order to set up the right environment. The following are the instructions.

<ul>

 <li>You need to have the Android SDK and Python 2.x (​not​x; Python 3.x versions are ​not compatible with the scripts provided.) installed on your machine. If you have not installed these, please do it first and proceed to the next step.</li>

 <li>Add &lt;your Android SDK directory&gt;/tools/bin to your $PATH so you can run Android’s development tools from anywhere.

  <ul>

   <li>To find out what your Android SDK directory is, click File -&gt; Settings (on Mac, Android Studio -&gt; Preferences), go to Appearance &amp; Behavior -&gt; System Settings -&gt; Android SDK. On the top right side, it will show your Android SDK location.</li>

  </ul></li>

</ul>

○    A good reference on how to change $PATH is <u>​</u><u><a href="https://www.java.com/en/download/help/path.xml">here</a></u><u>​</u><a href="https://www.java.com/en/download/help/path.xml">.</a>

<ul>

 <li>Add &lt;your Android SDK directory&gt;/platform-tools to your $PATH so you can run Android’s platform tools from anywhere.</li>

 <li>Add &lt;your Android SDK directory&gt;/emulator to your $PATH so you can run Android’s emulator from anywhere.</li>

 <li>Download and save ​<u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/create_avd.py">py</a></u><u>​</u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/create_avd.py">,</a> <u>​</u><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/run_avd.py">run_avd.py</a></u><u>​</u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/run_avd.py">,</a> and <u>​</u><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/set_redir.py">set_redir.py</a></u><u>​</u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/set_redir.py">.</a></li>

 <li>To create AVDs, enter: ​python create_avd.py 5 &lt;your Android SDK directory&gt;

  <ul>

   <li>The above command should be executed only once because you do not need to create AVDs multiple times.</li>

  </ul></li>

</ul>

○    In the middle of the script, it will ask “Do you wish to create a custom hardware profile [no]” multiple times. The script handles it automatically, so please do not enter anything to answer that question.

○    5 AVDs should have been created by the above command. The names are avd0, avd1, avd2, avd3, &amp; avd4. You can manipulate them in Android Studio, but please do not edit or delete them because they are necessary for our scripts to work.

○    If you can’t create x86-based AVDs, please enter: ​python create_avd.py -a arm 5 &lt;your Android SDK directory&gt;​ instead; this will create ARM-based AVDs.

However, we strongly encourage you to not do this, but to create x86 AVDs.

<ul>

 <li>For all the programming assignments except this first one, ​you will need to run 5 AVDs at the same time​. This means that you need to have access to a machine that can handle 5 AVDs running simultaneously.</li>

 <li>In order to test the above, please enter: ​python run_avd.py 5 ○ The above command will launch 5 AVDs.

  <ul>

   <li>Please play around with all 5 AVDs and make sure that your machine can handle them comfortably. Most of the recent laptops will run 5 AVDs without much difficulty.</li>

  </ul></li>

</ul>

○    After you are done checking, close all AVDs.

<ul>

 <li>For this assignment you need two AVDs, so enter: ​python run_avd.py 2 ○ The above command will start two AVDs, avd0 &amp; avd1.

  <ul>

   <li>In general, to run the AVDs created by create_avd.py, enter: ​python run_avd.py &lt;number of AVDs&gt;</li>

  </ul></li>

 <li>After all AVDs finish launching, create a network that connects the AVDs by entering: python set_redir.py 10000

  <ul>

   <li>The above command will set up port redirections, but there are some restrictions in terms of socket programming. We will detail the restrictions in Step 3 below.</li>

  </ul></li>

</ul>

<h1>Step 3: Writing the Messenger App</h1>

The actual implementation is writing the messenger app. For this, we have a project template you can import to Android Studio.

<ol>

 <li>Download <u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/SimpleMessenger.zip">the project template zip fil</a></u><u>​ </u><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/SimpleMessenger.zip">e</a></u> <u>​ </u>to a temporary directory.</li>

 <li>Extract the template zip file and copy it to your Android Studio projects directory.

  <ol>

   <li>Make sure that you copy the correct directory. After unzipping, the directory name should be “SimpleMessenger”, and right underneath, it should contain a number of directories and files such as “app”, “build”, “gradle”, “build.gradle”, “gradlew”, etc.</li>

  </ol></li>

 <li>After copying, delete the downloaded template zip file and unzipped directories and files.</li>

</ol>

This is to make sure that you do not submit the template you just downloaded. (There

were many people who did this before.)

<ol start="4">

 <li>Open the project template you just copied in Android Studio.</li>

 <li>Add your code to the project. If you look at the template code, there are a few “TODO” sections. Those are the places where you need to add your code.</li>

 <li>Before implementing anything, please understand the template code first.

  <ol>

   <li>The main Activity is in SimpleMessengerActivity.java.</li>

   <li>Please read the code and the comments carefully.</li>

  </ol></li>

</ol>




The project requirements are below. ​You must follow everything below exactly. Otherwise, you will get ​no point​ on this assignment. ​And when we say no point, we actually mean it ​:-)

<ol>

 <li>There should be only one app that you develop and need to install for grading. If you just use the project template and add your code there, you will be able to satisfy this requirement.</li>

 <li>When creating your new Android application project in Android Studio, use the following:</li>

</ol>

○    Application Name: SimpleMessenger

○    Project Name: SimpleMessenger

○    Package Name: edu.buffalo.cse.cse486586.simplemessenger ○    API level 19 as the minimum &amp; target SDK.

○    If you just use the project template, you will be able to satisfy this requirement.

<ol start="3">

 <li>There should be only one text box on screen where a user of the device can write a text message to the other device. If you just use the project template, you will satisfy this requirement.</li>

 <li>The other device should be able to display on screen what was received and vice versa.</li>

</ol>

The project template contains basic code for displaying messages on screen.

<ol start="5">

 <li>You need to use the Java Socket API.</li>

 <li>All communication should be over TCP.</li>

 <li>You can assume that the size of a message will never exceed 128 bytes (characters).</li>

</ol>




As mentioned above, the Android emulator environment is not flexible for networking among multiple AVDs. Although set_redir.py enables networking among multiple AVDs, it is very different from a typical networking setup. When you write your socket code, you have the following restrictions:

<ul>

 <li>In your app, you can open only one server socket that listens on port 10000 regardless of which AVD your app runs on.</li>

 <li>The app on avd0 can connect to the listening server socket of the app on avd1 by connecting to &lt;ip&gt;:&lt;port&gt; == 10.0.2.2:11112.</li>

 <li>The app on avd1 can connect to the listening server socket of the app on avd0 by connecting to &lt;ip&gt;:&lt;port&gt; == 10.0.2.2:11108.</li>

 <li>Your app knows which AVD it is running on via the following code snippet. If portStr is “5554”, then it is avd0. If portStr is “5556”, then it is avd1:</li>

</ul>

TelephonyManager tel =

(TelephonyManager) this.getSystemService(Context.TELEPHONY_SERVICE);

String portStr = tel.getLine1Number().substring(tel.getLine1Number().length() – 4);

<ul>

 <li>The project template already implements the above, but you are expected to understand the code as this is critical for the rest of the programming assignments.</li>

 <li><u><a href="https://developer.android.com/tools/devices/emulator.html#emulatornetworking">This document</a></u>​ explains the Android emulator networking environment in more detail.</li>

 <li>In general, set_redir.py creates an emulated, port-redirected network like this (VR stands for Virtual Router):</li>

</ul>




<h1>Testing</h1>

We have testing programs to help you see how your code does with our grading criteria. If you find any rough edge with the testing programs, please report it on Piazza so the teaching staff can fix it. The instructions are the following:

<ol>

 <li>Download a testing program for your platform. If your platform does not run it, please report it on Piazza.

  <ol start="8">

   <li><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/simplemessenger-grading.exe">Windows</a></u>​: We’ve tested it on 64-bit Windows 8.</li>

   <li><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/simplemessenger-grading.linux">Linux</a></u>:​ We’ve tested it on 64-bit Ubuntu 14.04.</li>

   <li><u><a href="http://www.cse.buffalo.edu/~stevko/courses/cse486/spring19/files/simplemessenger-grading.osx">OS X</a></u>​: We’ve tested it on 64-bit OS X 10.9 Mavericks.</li>

  </ol></li>

 <li>Before you run the program, please make sure that you are running two AVDs (avd0 &amp; avd1). ​python run_avd.py 2​ will do it.</li>

 <li>Please also make sure that you have installed your SimpleMessenger on those two AVDs.</li>

 <li>Run the testing program from the command line.</li>

 <li>At the end of the run, it will give you one of the three outputs.

  <ol>

   <li>No communication verified: if SimpleMessenger instances cannot communicate with each other. This is 0 point.</li>

   <li>One-way communication verified: if SimpleMessenger on avd0 can send a message to SimpleMessenger on avd1. This is 2 points.</li>

   <li>Two-way communication verified: if both AVDs can communicate with each other. This is additional 3 points.</li>

  </ol></li>

</ol>