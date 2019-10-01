# Unlockme.apk

## Solution

1. Install Unlockme.apk in a rooted Android device
2. Scan a human face successfully in order view the login page
3. Decode APK file using `apktool` to find the hardcoded, base64 encoded, password
4. Do a source code analysis to understand the login process
   1. `register()` function was probably not being called, even though the code did exist
   2. `registerUser()` function was being invoked from within the `register()` function, based on a certain condition
   3. The app was trying to read user details from a shared preferences file named as `ctf.xml`.
5. Next obvious things to do was
   1. Update the shared preferences file `ctf.xml` to include following missing details `keyusername`, `true`, and `keyemail`
   2. Call the `registerUser()` function directly using Frida tool
   3. If all goes well, the `Internal` activity would be displayed
6. Analyse the `Internal.class` source code to understand what is happening
   * `startTimer()` function in class `Internal` is instantiating the class `Internal$1`
   * The source code in `Internal$1.class` file has a reference to a native method called `stringFromJNI()`
   * The source code in `Internal.class` file is loading a library named as `hello-jni`.
7. Using Frida, call the `startTimer()` function of `Internal` class.
8. Print the string value returned when `stringFromJNI()` function is called, in order to read the flag.