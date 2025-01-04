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
On Ubuntu ( use following in Root folder. Where Root folder is J7app )

    ./gradlew assembleRelease 
    or
    gradle assembleRelease 

On Windows ( use following in Root folder. Where Root folder is J7app )

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

Step K1: Generate the Keystore File

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

Step K2: Using the Keystore

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

Step K3: Verify Keystore

Check if the keystore was created successfully:

        keytool -list -v -keystore my-release-key.jks

Replace the file name and passwords with your values as needed.

keytool command is not always available directly in the command line unless the Java Development Kit (JDK) is properly installed and configured. Here’s how to ensure keytool is accessible on a Windows machine:


---

Step K4: Ensure JDK is Installed

1. Install JDK if it is not already installed:

Download from Oracle JDK or use an open-source version like OpenJDK.



2. Confirm installation by running:

        java -version

---

Step K5: Locate keytool

The keytool utility is typically located in the bin directory of the JDK installation:

        Example path: C:\Program Files\Java\jdk-17\bin






---

Step  K6: Add keytool to the Path

1. Open System Properties:
Right-click This PC → Properties → Advanced system settings → Environment Variables.


2. Under System Variables, find Path, click Edit, and add the path to the JDK bin folder:

        C:\Program Files\Java\jdk-17\bin


3. Click OK to save the changes.




---

Step K7: Verify keytool is Available

Open a new Command Prompt and run:

        keytool -help

If correctly set, this will display the keytool help information.

@@ Ubuntu 22.04 Machine

Steps can be adapted for Ubuntu 22.04, though the commands differ slightly for installing packages and setting up paths. Here’s the corresponding guide for Ubuntu:


---

Step U1: Install JDK

1. Install OpenJDK (version 11 or 17, depending on your project requirement):

        sudo apt update
        sudo apt install openjdk-17-jdk


2. Set environment variables by editing ~/.bashrc or ~/.zshrc:

        echo "export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64" >> ~/.bashrc
        echo "export PATH=\$PATH:\$JAVA_HOME/bin" >> ~/.bashrc
        source ~/.bashrc


3. Verify installation:

        java -version




---

Step U2: Install Android SDK (Command-Line Tools)

1. Download the command-line tools from the Android SDK page.


2. Extract the tools:

        mkdir -p ~/Android/Sdk
        unzip commandlinetools-linux-*.zip -d ~/Android/Sdk/cmdline-tools
        mv ~/Android/Sdk/cmdline-tools/cmdline-tools ~/Android/Sdk/cmdline-tools/latest


3. Set environment variables in ~/.bashrc:

        echo "export ANDROID_HOME=~/Android/Sdk" >> ~/.bashrc
        echo "export PATH=\$PATH:\$ANDROID_HOME/platform-tools:\$ANDROID_HOME/cmdline-tools/latest/bin" >> ~/.bashrc
        source ~/.bashrc


4. Install essential packages:

        sdkmanager --install "platform-tools" "platforms;android-33"




---

Step U3: Install Android NDK

1. Use sdkmanager to install NDK:

        sdkmanager --install "ndk;25.1.8937393"


2. Verify NDK installation:

        ls $ANDROID_HOME/ndk




---

Step U4: Install Gradle

1. Download Gradle from Gradle’s website.


2. Extract it:

        wget https://services.gradle.org/distributions/gradle-9.0-bin.zip
        sudo unzip gradle-9.0-bin.zip -d /opt/gradle


3. Set environment variables in ~/.bashrc:

        echo "export GRADLE_HOME=/opt/gradle/gradle-9.0" >> ~/.bashrc
        echo "export PATH=\$PATH:\$GRADLE_HOME/bin" >> ~/.bashrc
        source ~/.bashrc


4. Verify installation:

        gradle -v

---

Commands to Build APK on Ubuntu

In your project directory (J7appv4), run:

        ./gradlew assembleRelease
          or
         gradle assembleRelease

    This will generate the APK in app/build/outputs/apk/release/.


In Ubuntu, the keytool command is part of the Java Development Kit (JDK). If keytool is not available, you need to install the JDK and configure it properly.


---

Step U5: Install OpenJDK (if needed)

1. Update the package index:

        sudo apt update


2. Install the OpenJDK (choose version 11 or 17):

        sudo apt install openjdk-17-jdk


3. Confirm installation:

        java -version




---

Step U6: Find keytool

The keytool binary is located in the bin directory of the JDK installation:

Path example: /usr/lib/jvm/java-17-openjdk-amd64/bin/keytool



---

Step U7: Add keytool to PATH

1. Edit your shell configuration file (~/.bashrc or ~/.zshrc):

        echo "export PATH=\$PATH:/usr/lib/jvm/java-17-openjdk-amd64/bin" >> ~/.bashrc
        source ~/.bashrc


2. Verify the keytool is available:

        keytool -help

---

Using keytool to Generate a Keystore

Run this command to create a keystore:

keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias

This command works the same as on Windows, but ensure paths and configurations match your environment.
