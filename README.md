# Ghost ROM #

## Setting up your build environment ##
To setup your build environment and sync Ghost ROM, please follow the guide below.

1) If doing a fresh install, skip to step 2. Otherwise, do the following:

```bash
sudo apt-get remove openjdk-* icedtea-* icedtea6-
```
If necessary, follow the on-screen instructions to remove any stray Java versions. Otherwise, move on to the next step.

<br />

2) Install the main build tools with this command:
```bash
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl \
zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev \
x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils \
xsltproc unzip
```

<br />

3) To install Java:

```bash
sudo apt-get update
sudo apt-get install openjdk-8-jdk
sudo apt-get install openjdk-8-jre
```

<br />

4) Install “repo”. Recommend doing 4 separate commands here:
```bash
curl https://storage.googleapis.com/git-repo-downloads/repo > repo
```
```bash
chmod a+x repo
```
```bash
sudo install repo /usr/local/bin
```
```bash
rm repo

```

<br />

5) Set some global defaults for your Android build environment within bash:
```bash
nano ~/.bashrc
```

At the very bottom (use the Page Down key) paste this code to a new line:
```bash
Code to add to bashrc:
export PATH=~/bin:$PATH
export USE_CCACHE=1
export USE_PREBUILT_CACHE=1
export PREBUILT_CACHE_DIR=~/.ccache
```
Save it. In nano, that would be Ctrl-O and then Enter. Then Ctrl-X to exit back to terminal.

<br />

6) Set your ccache size:
```bash
ccache -M 100G
```

<br />

7) Restart bash:
```bash
source ~/.bashrc
```

<br />

8) In the terminal, navigate to where you would like to download the Ghost ROM source code. The commands below will make it in your home folder, but if you have limited space you may want to create it somewhere else. Faster is better, i.e. SSD would be best, USB external (even 3.0) will be comparatively slow. Here we go:
```bash
mkdir ~/ghostrom
cd ~/ghostrom
```

<br />

9) Now you're going to initialize the repo:
```bash
repo init -u https://github.com/ghostrom/manifest -b oreo
```

<br />

10) Last step. Time to get the source, this part will take a while and will vary depending on your PC and internet speed:
```bash
repo sync
```

If using Mint, you will need to install support for lz4 compression using the following command:
```bash
sudo apt-get install liblz4-tool
```

Build environment setup done!

<br />

## Permissions ##
Don’t forget to set up permissions for adb/fastboot - 51-android.rules!
See [this link](https://developer.android.com/studio/run/device.html) - scroll down to the "udev" section. Follow the steps where it talks about "51-android.rules".

That's it! Everything should be ready to go!
