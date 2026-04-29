# Installation

Installer le [plugin Flutter pour VSCode](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter).

Cette extension ajoute un support pour l'édition, la refactorisation, l'exécution et le rechargement efficaces des applications mobiles Flutter. Elle installera automatiquement l'extension pour langage de programmation Dart dont elle dépend.

Tester la bonne installation avec la commande `flutter doctor`. (Ctrl + Maj + P pour ouvrir la palette de commande de VSCode).

```shell
flutter doctor -v

[✓] Flutter (Channel stable, 3.29.3, on Fedora Linux 42 (Adams) 6.14.5-300.fc42.x86_64, locale fr_FR.UTF-8) [149ms]
    • Flutter version 3.29.3 on channel stable at /opt/flutter
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision ea121f8859 (il y a 4 semaines), 2025-04-11 19:10:07 +0000
    • Engine revision cf56914b32
    • Dart version 3.7.2
    • DevTools version 2.42.3

[✓] Android toolchain - develop for Android devices (Android SDK version 36.0.0) [1 098ms]
    • Android SDK at /usr/local/android-sdk
    • Platform android-36, build-tools 36.0.0
    • ANDROID_HOME = /usr/local/android-sdk
    • Java binary at: /usr/local/android-studio/jbr/bin/java
      This is the JDK bundled with the latest Android Studio installation on this machine.
      To manually set the JDK path, use: `flutter config --jdk-dir="path/to/jdk"`.
    • Java version OpenJDK Runtime Environment (build 21.0.5+-12932927-b750.29)
    • All Android licenses accepted.

[✓] Chrome - develop for the web [81ms]
    • CHROME_EXECUTABLE = /usr/bin/chromium-browser

[✗] Linux toolchain - develop for Linux desktop [146ms]
    ✗ clang++ is required for Linux development.
      It is likely available from your distribution (e.g.: apt install clang), or can be downloaded from
      https://releases.llvm.org/
    ✗ CMake is required for Linux development.
      It is likely available from your distribution (e.g.: apt install cmake), or can be downloaded from
      https://cmake.org/download/
    ✗ ninja is required for Linux development.
      It is likely available from your distribution (e.g.: apt install ninja-build), or can be downloaded from
      https://github.com/ninja-build/ninja/releases
    • pkg-config version 2.3.0
    ✗ GTK 3.0 development libraries are required for Linux development.
      They are likely available from your distribution (e.g.: apt install libgtk-3-dev)

[✓] Android Studio (version 2024.3) [78ms]
    • Android Studio at /usr/local/android-studio
    • Flutter plugin version 85.0.4
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 21.0.5+-12932927-b750.29)

[✓] Connected device (3 available) [216ms]
    • sdk gphone64 x86 64 (mobile) • emulator-5554 • android-x64    • Android 16 (API 36) (emulator)
    • Linux (desktop)              • linux         • linux-x64      • Fedora Linux 42 (Adams) 6.14.5-300.fc42.x86_64
    • Chrome (web)                 • chrome        • web-javascript • Chromium 136.0.7103.59 Fedora Project

[✓] Network resources [1 006ms]
    • All expected network resources are available.

! Doctor found issues in 1 category.
```
