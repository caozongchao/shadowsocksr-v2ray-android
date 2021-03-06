## A ShadowsocksR and V2Ray Client for Android

A [shadowsocksR](https://github.com/breakwa11/shadowsocks-rss/) and [V2Ray](https://github.com/v2ray/v2ray-core) client for Android, integrate SSR and V2Ray in one application, written in Scala.

 ![build](https://github.com/xxf098/shadowsocksr-v2ray-android/workflows/build/badge.svg?branch=xxf098%2Fmaster&event=push) 
 [![GitHub release](https://img.shields.io/github/release/xxf098/shadowsocksr-v2ray-android)](https://github.com/xxf098/shadowsocksr-v2ray-android/releases) 
 [![GitHub issues](https://img.shields.io/github/issues/xxf098/shadowsocksr-v2ray-android.svg)](https://GitHub.com/xxf098/shadowsocksr-v2ray-android/issues/) 
 [![Gitter](https://badges.gitter.im/shadowsocksr-v2ray-android/community.svg)](https://gitter.im/shadowsocksr-v2ray-android/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)


### PREREQUISITES

* JDK 1.8
* SBT 0.13.8
* Android SDK
  - Build Tools 29+
  - Android Support Repository and Google Repository (see `build.sbt` for version)
* Android NDK r12b `High version may case something build fail`

### BUILD with Android Studio

*Warnning: Cannot build in windows*

* Download [Android Studio](https://developer.android.com/studio)
* Download [Android NDK r12b](https://developer.android.com/ndk/downloads/older_releases)
* Set proxy for sbt in Android Studio: open `Settings -> Build, Execution, Deployment -> Build Tool -> sbt`, in `VM parameters` input (or Welcome Page `Configure -> Edit Custom VM Options`):

        -Dhttp.proxyHost=127.0.0.1
        -Dhttp.proxyPort=8080
        -Dhttps.proxyHost=127.0.0.1
        -Dhttps.proxyPort=8080
        
* Set environment variable `ANDROID_HOME` to `/path/to/Android/Sdk`
* Set environment variable `ANDROID_NDK_HOME` to `/path/to/Android/android-ndk-r12b`
* Set environment variable `TERM` to `xterm-color`
* Create your key following the instructions at https://developer.android.com/studio/publish/app-signing.html
* Put your key in ~/.keystore or any other place
* Create `local.properties` from `local.properties.example` with your own key information

        key.alias: abc
        key.store: /path/to/Android/abc.jks
        key.store.password: abc

* if you installed multiple versions of Java, use `sudo update-alternatives --config java` to select Java 8
* Before build apk, make sure inside `./project/build.properties`, sbt.version=0.13.18 
* Invoke the building like this

```bash
    export https_proxy=http://127.0.0.1:8080
    export ANDROID_HOME=/path/to/Android/Sdk
    export ANDROID_NDK_HOME=/path/to/Android/android-ndk-r12b
    export TERM=xterm-color
    # install and update all git submodule
    git submodule update --init
    # Build the App
    sbt native-build clean android:package-release
    # run app
    sbt android:run
```

##### If you use x64 linux like Archlinux x86_64, or your linux have new version ncurses lib, you may need install the 32bit version ncurses and link it as follow (make sure all these *.so files in the right location under your system, otherwise you have to copy them to /usr/lib/ and /usr/lib32/ directory):

```bash
    # use Archlinux x86_64 as example
    
    # install ncurses x64 and x86 version
    sudo pacman -S lib32-ncurses ncurses
    
    # link the version-6 ncurses to version-5
    sudo ln -s /usr/lib/libncursesw.so /usr/lib/libncurses.so.5
    sudo ln -s /usr/lib32/libncursesw.so /usr/lib32/libncurses.so.5
    
    # link libncurses to libtinfo
    sudo ln -s /usr/lib/libncurses.so.5 /usr/lib/libtinfo.so.5
    sudo ln -s /usr/lib32/libncurses.so.5 /usr/lib32/libtinfo.so.5
```

#### Integration with Android Studio

Checkout this [link](http://srodrigo.me/setting-up-scala-on-android/)
* rm -rf ~/.android/sbt/exploded-aars/*
* In Project Settings -> Modules -> shadowsocksr, change manifest file path
* In Run/Debug Configuration -> Before launch, replace `Gradle-aware Make` with `android:run`

#### BUILD on Mac OS X (with HomeBrew)

* Install Android SDK and NDK by run `brew install android-ndk android-sdk`
* Add `export ANDROID_HOME=/usr/local/Cellar/android-sdk/$version` to your .bashrc , then reopen the shell to load it.
* Add `export ANDROID_NDK_HOME=/usr/local/Cellar/android-ndk/$version` to your .bashrc , then reopen the shell to load it.
* echo "y" | android update sdk --filter tools,platform-tools,build-tools-23.0.2,android-23,extra-google-m2repository --no-ui -a
* echo "y" | android update sdk --filter extra-android-m2repository --no-ui --no-https -a
* Create your key following the instructions at http://developer.android.com/guide/publishing/app-signing.html#cert
* Put your key in ~/.keystore
* Create `local.properties` from `local.properties.example` with your own key information .
* Invoke the building like this

```bash
    git submodule update --init

    # Build native binaries
    ./build.sh

    # Build the apk
    sbt clean android:package-release
```

## OPEN SOURCE LICENSES

* shadowsocks-libev: [GPLv3](https://github.com/shadowsocks/shadowsocks-libev/blob/master/LICENSE)
* tun2socks: [BSD](https://github.com/shadowsocks/badvpn/blob/shadowsocks-android/COPYING)
* redsocks: [APL 2.0](https://github.com/shadowsocks/redsocks/blob/master/README)
* OpenSSL: [OpenSSL](https://github.com/shadowsocks/openssl-android/blob/master/NOTICE)
* pdnsd: [GPLv3](https://github.com/shadowsocks/shadowsocks-android/blob/master/src/main/jni/pdnsd/COPYING)
* libev: [GPLv2](https://github.com/shadowsocks/shadowsocks-android/blob/master/src/main/jni/libev/LICENSE)
* libevent: [BSD](https://github.com/shadowsocks/libevent/blob/master/LICENSE)
* v2ray-core: [BSD](https://github.com/v2ray/v2ray-core/blob/master/LICENSE)
* go-tun2socks: [BSD](https://github.com/eycorsican/go-tun2socks/blob/master/LICENSE)

### LICENSE

Copyright (C) 2016 by Max Lv <<max.c.lv@gmail.com>> <br/>
Copyright (C) 2016 by Mygod Studio <<mygodstudio@gmail.com>>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
