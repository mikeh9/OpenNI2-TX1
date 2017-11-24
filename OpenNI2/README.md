# OpenNI

Website: http://structure.io/openni

## Contributing

Pull requests that do not apply cleanly on top of the [`develop` branch head](http://github.com/occipital/OpenNI2/tree/develop) will be rejected.

Other than that, sensible and meaningful contributions are very welcome!

## Building for Mac OS X

### Build Prerequisites

  - **Libusb 1.0**

    First, install **Homebrew**, if you do not have it already:
    	
    	ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

	Then install **libusb** with it:

    	brew install libusb --universal

### Build Instructions

Run: `make`

## Building for Windows

### Build Prerequisites

Download and install the following windows software:

  - [Microsoft Visual Studio 2010](http://msdn.microsoft.com/en-us/vstudio/bb984878.aspx)
  - [Microsoft Kinect SDK v1.6](http://go.microsoft.com/fwlink/?LinkID=262831)
  - [Python 2.6+/3.x](http://www.python.org/download/)
  - [PyWin32](http://sourceforge.net/projects/pywin32/files/pywin32/)

	Please make sure you download the version that matches your exact python version.
  - [JDK 6.0](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u32-downloads-1594644.html)

    You must also define an environment variable called `JAVA_HOME` that points to the JDK installation directory. For example:
    
		set JAVA_HOME=c:\Program Files (x86)\Java\jdk1.6.0_32
  - [WIX 3.5](http://wix.codeplex.com/releases/view/60102)
  - [Doxygen](http://www.stack.nl/~dimitri/doxygen/download.html#latestsrc)
  - [GraphViz](http://www.graphviz.org/Download_windows.php)

### Build Instructions

Build the Visual Studio solution `OpenNI.sln`.

## Building for Linux

### Build Prerequisites (Ubuntu & Debian)

Download and install the following packages, using apt:
  
	sudo apt-get install \
		g++              \
		python           \
		libusb-1.0-0-dev \
		libudev-dev      \
		openjdk-6-jdk    \
		freeglut3-dev    \
		doxygen          \
		graphviz

### Build Prerequisites (Other Distributions)

  Download and install the following Linux software:
  
  - [GCC 4.x](http://gcc.gnu.org/releases.html)
  - [Python 2.6+/3.x](http://www.python.org/download/)
  - [LibUSB 1.0.x](http://sourceforge.net/projects/libusb/files/libusb-1.0/)
  - [LibUDEV](http://www.freedesktop.org/wiki/Software/systemd/)
  - [JDK 6.0](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u32-downloads-1594644.html)
  - [FreeGLUT3](http://freeglut.sourceforge.net/index.php#download)
  - [Doxygen](http://www.stack.nl/~dimitri/doxygen/download.html#latestsrc)
  - [GraphViz](http://www.graphviz.org/Download_linux_ubuntu.php)

### Build Instructions

Run: `make`

### Cross-Compiling for ARM

  The following environment variables should be defined:

  - `ARM_CXX=<path to cross-compilation g++>`
  - `ARM_STAGING=<path to cross-compilation staging dir>`

  Then, run:

		PLATFORM=Arm make

## Building for Android

These instructions assume a device running **Android KitKat**. The samples NiViewer, SimpleRead, and SimpleViewer were tested and found to run succesfully on a Nexus 7 running Android 4.4.4.  **Please** ensure you are using a high quality USB OTG cable!

Please refer to [this issue](https://github.com/occipital/OpenNI2/issues/43) for updated information regarding OpenNI2 on **Android Lollipop**.

The build instructions presented here focus on **Eclipse** with the **ADT plugin**. As of the May 2015 Android Studio's NDK support continues to be reported as incomplete and is therefore not recommended as a build environment.

### Build Prerequisites (All Hosts)

  - Download and install the latest [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
  - Install the **Android SDK**:
	- Download the [Android SDK](http://developer.android.com/sdk/index.html#Other), making sure you download the appropriate SDK Tools Only package for your host platform.
    - Follow [these instructions](http://developer.android.com/sdk/installing/index.html?pkg=tools) for installing the stand-alone Android SDK Tools.
    - Follow [these instructions](http://developer.android.com/sdk/installing/adding-packages.html) for adding Android SDK packages. 
    - Define the `ANDROID_HOME` environment variable pointing to the SDK installation directory.
  - Install the **Android NDK**:
    - Download the lastest [Android NDK](http://developer.android.com/tools/sdk/ndk/index.html#Downloads) and follow [these instructions](http://developer.android.com/tools/sdk/ndk/index.html#installing) for installing it.
    - Define the `NDK_HOME` environment variable pointing to the NDK installation directory. 
  - Install **Eclipse**:
    - Download the latest [Eclipse](http://www.eclipse.org/downloads/) release for your host platform.
    - Go to `Eclipse → Preferences → Android → NDK` and set the correct NDK Location.
  - Install the **Eclipse ADT plugin**:
    - Follow [these instructions](http://developer.android.com/sdk/installing/installing-adt.html) for downloading and configuring the Eclipse ADT plugin.

### Build Prerequisites (Windows Hosts)

  - Download and install the following Windows software:
    - [JDK 6.0](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u32-downloads-1594644.html)
    - [Ant](https://code.google.com/p/winant)
  - Define the `JAVA_HOME` environment variable, pointing to the correct JDK installation directory. For example:

		set JAVA_HOME=c:\Program Files (x86)\Java\jdk1.6.0_32

### Build Prerequisites (Ubuntu & Debian Linux Hosts)

Download and install the following packages, using apt:
  
	sudo apt-get install \
		openjdk-6-jdk    \
		ant

### Build Prerequisites (Other Linux Hosts)

Download and install the following Linux software:

- [JDK 6.0](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u32-downloads-1594644.html)
- [Ant](http://ant.apache.org/)


### Build Instructions (All Hosts)

  - Go to `Eclipse -> Import... -> Android -> Existing Android Code Into Workspace`
  - Select the root directory of OpenNI2.
  - Projects found should include:
    - `NiViewer`
    - `OpenNIForAndroid`
    - `SimpleRead`
    - `SimpleViewer`
  - Set the Project Build Target for all imported projects.


## Packaging

- Go into the directory `Packaging`
- Run `ReleaseVersion.py [x86|x64|Arm|Android]`
- Installer will be placed in the `Final` directory
- Android Specific: `keytool` was used as follows to generate a generic keystore for the Android build products:  
	- `keytool -genkey -v -keystore ./<appname>.keystore -alias NiVKey -keyalg RSA -keypass android -storepass android -keysize 2048 -validity 10000`


