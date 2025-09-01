## WPILib Installation

For a more comprehensive installation guide, visit the [WPILib docs](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html). Otherwise, follow the appropriate guide below. All installers can be found on [the latest GitHub WPILib release](https://github.com/wpilibsuite/allwpilib/releases/).

### Windows

1. Scroll down to the downloads section of the latest release and select the Windows option.
2. Extract the installer `.iso` file by right clicking it and selecting `Mount` or by installing [7-Zip](https://www.7-zip.org/download.html) and using the `7-Zip > Extract to WPILib_Windows64-<VERSION_DATE>\` option.
3. Run the `WPILibInstaller.exe`.
4. Follow the general instructions below

### Linux

1. Download the `Linux (x64)` file in the latest release. 
2. Run the following commands in the folder you downloaded the file in

```sh
tar -xf WPILib_Linux-<version>.tar.gz
cd WPILib_Linux-<version>/
./WPILibInstaller
```

_Post-installation ***note***: Some Linux distributions will require you to give opening permissions for `.desktop` files. To give these permissions, simply run `chmod a+x <PATH_TO_DESKTOP_FILE>`. To start the application, some distributions like Ubuntu have built in launchers (opened by pressing `super`); otherwise, install a program like [rofi](https://github.com/davatorium/rofi)._

### General 

- When you are asked to select the install mode you would like, select `Everything`.
- The installer will ask you how you would like to install/handle the VSCode installation. It is easiest if you select `Download for this computer only (fastest)`, regadless of your OS or distro.
- This year, we will be using Java for all robot programming. Please follow the Java installation guide on your newly installed WPILib VSCode IDE.

## Java Installation

> [!NOTE]
> The following Java installation instructions assume that you are using the WPILib provided version of VSCode. Other IDEs will have a fairly similar instllation process, but they will not be covered here.

### Windows

Visit the [installation page](https://learn.microsoft.com/en-us/java/openjdk/download) and use the `.msi` installer to download the jdk. Open up your terminal and try the following commands to identify the jdk installation location:

```
where javac
echo %JAVA_HOME%
```

One of the commands should output something like `C:\Program Files\Java\jdk-17\bin\javac.exe` or `C:\Program Files\OpenJDK\jdk-17`. Only include the part up to `jdk-17` when putting your Java path in VSCode. Finally, in your VSCode `settings.json` (`Ctrl+Shift+P` then type and select the option `Preferences: Open User Settings (JSON)`), include the following line with the appropriate jdk installation path.

```json
  "java.home": "<JDK_PATH>",
```

### Linux

#### Install the JDK:
As of now, WPILib primarily supports Java 17, so we will have to explicitly install an older version of Java.
Arch: `yay -S jdk17-openjdk` (or your AUR helper of choice)
Debian: `sudo apt-get install openjdk-17-jdk`

#### Identify the installation location and link the path
Assuming you only have one jdk installed, the command `dirname $(dirname $(readlink -f $(which javac)))` will output the location of your jdk. It should look something like `/usr/lib/jvm/java-17-openjdk`. In that case, you are safe to just put the following into your `settings.json` file (`Ctrl+Shift+P` then type and select the option `Preferences: Open User Settings (JSON)`).

```json
  "java.home": "<JDK_PATH>",
```

If you already have a different version of Java installed, and the previous command printed something like `/usr/lib/jvm/java-24-jdk`, you can also add the following to your config so the integrated terminal uses the correct Java version. If for some reason you installed a Java 17 JDK from a different source, more often than not, you can find your jdk path by running `ls /usr/lib/jvm`.

```json
  "terminal.integrated.env.linux": {
    "JAVA_HOME": "<JDK_PATH>",
    "PATH": "<JDK_PATH>/bin:${env:PATH}"
  },
```

If you ever plan on running commands for FRC outside of the WPILib integrated terminal, you can add the following to your shell configuration file (probably `.bashrc` in your `$HOME` directory).

```sh
  export JAVA_HOME="<JDK_PATH>"
  export PATH="$JAVA_HOME/bin:$PATH"
```

#### Verify your installation
Run `java -version` to verify that you have properly installed Java and that it is using version 17.
