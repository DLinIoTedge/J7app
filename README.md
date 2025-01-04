# J7app

---


J7app is an innovative Android application designed to deliver high-performance solutions by leveraging a hybrid architecture with Java and C++ for computational tasks. This project is built using the Android SDK and Android NDK, providing an efficient and scalable platform for modern mobile development. By focusing on optimized native code execution on the CPU, J7app ensures enhanced performance and faster processing for resource-intensive operations.

---

Key Features

Seamless Integration of Java and C++: Utilize the power of the Android NDK for performance-critical components.

Robust Build System with Gradle: Simplified dependency management and flexible build customization.
Modular Codebase: Clean and maintainable project structure with a focus on scalability.
Efficient CPU Utilization: Native code optimization for computational tasks.


---

Project Structure

Root Folder (J7appv4): Contains project-level configuration files (build.gradle, settings.gradle, gradle.properties).

Gradle Wrapper: Uses gradle-wrapper.properties for specifying Gradle version (9.0).
App Folder: Includes the src directory, build.gradle, and key file for signing the APK.

---

Build Instructions
To build the release APK from the command line:
On Ubuntu

    ./gradlew assembleRelease

On Windows

    gradlew assembleRelease


---

This repository is ideal for developers aiming to understand and implement a hybrid Android application architecture using native C++ for performance optimization. Explore the code, contribute, or customize it to meet your project’s requirements.

# Prerequisites

##  for Windows machine

Here’s how to install the four prerequisites on a Windows machine via command line or PowerShell, including setting them in the Path.

Step 1: Install JDK

1. Download the JDK installer for Windows from Oracle’s website. Use curl or a browser to get the URL for the latest JDK version.


2. Run the installer silently:

        curl -o jdk-17-windows-x64.exe "https://download.oracle.com/java/17/latest/jdk-17_windows- x64_bin.exe"
        start /wait jdk-17-windows-x64.exe /s


3. Set environment variables:

        setx JAVA_HOME "C:\Program Files\Java\jdk-17" /M
        setx PATH "%PATH%;%JAVA_HOME%\bin" /M




---

Step 2: Install Android SDK (Command-Line Tools)

1. Download CLI tools from Android SDK.

2. Extract and move the tools to a directory, for example, C:\Android\Sdk.

        mkdir C:\Android\Sdk
        tar -xf commandlinetools-win-xxxx_latest.zip -C C:\Android\Sdk


3. Set environment variables:

        setx ANDROID_HOME "C:\Android\Sdk" /M
        setx PATH "%PATH%;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools" /M




---

Step 3: Install Android NDK

1. Use the SDK Manager to install NDK:

        sdkmanager --install "ndk;25.1.8937393"


2. Set NDK_HOME (optional if used directly in local.properties):

        setx NDK_HOME "%ANDROID_HOME%\ndk\25.1.8937393" /M




---

Step 4: Install Gradle

1. Download Gradle from Gradle’s website.


2. Extract Gradle to C:\Gradle.

        mkdir C:\Gradle
        tar -xf gradle-9.0-bin.zip -C C:\Gradle


3. Set environment variables:

        setx GRADLE_HOME "C:\Gradle\gradle-9.0" /M
        setx PATH "%PATH%;%GRADLE_HOME%\bin" /M




---

Verifying Installation

Check if everything is correctly installed:

        java -version
        gradle -v
        sdkmanager --list

These steps configure the required tools and ensure the command-line environment is ready to build your APK with gradlew.bat.

To build a key file (keystore) for signing an APK on a Windows machine, follow these steps using the keytool command:


---

Step 1: Generate the Keystore File

1. Open a Command Prompt or PowerShell window.


2. Run the following command to create a keystore:

        keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias

Explanation:

my-release-key.jks: The name of your keystore file (choose any name).

-keyalg RSA: Specifies the algorithm to use (RSA is recommended).

-keysize 2048: Sets the key size to 2048 bits.

-validity 10000: Sets the validity period of the key in days (adjust as needed).

-alias my-key-alias: The alias name for your key (choose any name).



3. Enter the required information:

Password for the keystore and key.

Your name, organization, location, etc.



4. The my-release-key.jks file will be created in the current directory.




---

Step 2: Using the Keystore

1. Place my-release-key.jks in a secure location (e.g., project’s app folder).


2. Reference the keystore in your build.gradle file:

        android {
            signingConfigs {
                release {
                    keyAlias 'my-key-alias'
                    keyPassword 'your-key-password'
                    storeFile file('my-release-key.jks')
                    storePassword 'your-store-password'
                }
            }
            buildTypes {
                release {
                    signingConfig signingConfigs.release
                    minifyEnabled false
                }
            }
        }




---

Step 3: Verify Keystore

Check if the keystore was created successfully:

keytool -list -v -keystore my-release-key.jks

Replace the file name and passwords with your values as needed.


