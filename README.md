# Android SDK Minimal Setup

> 📘 Also available in [Portuguese](README.pt-br.md)


> 📱 Minimal setup for Android SDK and Emulator, without relying on Android Studio.  
> 💡 Perfect for lightweight environments, automation, WSL, containers, or any IDE (VSCode, Neovim, JetBrains, Cursor) where installing Android Studio just for SDK access isn't necessary.

---

## 📦 Download the SDK

Access the official tools: [Command-line tools only](https://developer.android.com/studio#command-line-tools-only)  
Extract the contents to a folder like `.android-sdk/cmdline-tools/latest`:

```bash
.
└── .android-sdk
    └── cmdline-tools
        └── latest
            ├── bin
            └── lib
```

---

## ⚙️ Set Environment Variables

### Windows

```bat
REM Android
set ANDROID_HOME=%HOMEPATH%\.android-sdk
set PATH=%PATH%;%ANDROID_HOME%\cmdline-tools\latest\bin;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\emulator

REM Java
set JAVA_HOME=C:\tools\java\jdk\lts\jdk-21.0.2
set PATH=%PATH%;%JAVA_HOME%\bin
```

### Linux

```bash
# Android
export ANDROID_HOME=$HOME/.android-sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/emulator

# Java
export JAVA_HOME=$HOME/.jdk-21.0.2
export PATH=$PATH:$JAVA_HOME/bin
```

---

## 🔧 Install SDK Components

Run:

```bash
sdkmanager --update
sdkmanager "cmdline-tools;latest"
```

> ⚠️ If it creates a `latest-2` folder, remove the old one and rename the new to `latest`.

Then install the components:

```bash
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "system-images;android-36;google_apis;x86_64"
sdkmanager "emulator"
```

---

## 📱 Create and Run an Emulator

Create a new AVD:

```bash
avdmanager create avd --name "DevPixel36" --device "pixel_6" --package "system-images;android-36;google_apis;x86_64" --sdcard 512M --force
```

Run the emulator:

```bash
emulator -avd DevPixel36
```

Useful options:

```bash
emulator -avd DevPixel36 -no-snapshot -memory 2048 -gpu auto
```

Headless / background execution (e.g., for CI):

```bash
emulator -avd DevPixel36 -no-window -no-audio -no-boot-anim &
```

---

## 🛠️ Emulator Visual Fixes

If it starts off-screen or scaled incorrectly:

```bash
emulator -avd DevPixel36 -scale 0.75
```

Or force a specific screen size:

```bash
emulator -avd DevPixel36 -skin 720x1280
```

---

## ✍️ Author

George Colber  
[george@colber.com.br](mailto:george@colber.com.br)

---

## 📘 License

MIT License – feel free to use, adapt, and share!
