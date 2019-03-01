# Build instructions
## Requirements
* Ubuntu 16.04
* 200GB of hard drive space
* 8GB of RAM

## Build environment
### Packages
Install the following packages using `apt install`:

`bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-dev libxml2 libxml2-utils lzop openjdk-8-jdk pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev`

### Repo tool
Install the `repo` tool by running the following:
```
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
echo 'PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Fetching the sources
A directory to house the source code needs to be made. `~/comma_neos_sdm845` will be used in this example.
Run the following (the `repo sync` command will take a while):
```
mkdir ~/comma_neos_sdm845
cd ~/comma_neos_sdm845
repo init -u https://github.com/commaai/android.git -b sdm845
repo sync -c -j$(nproc)
```

## Building
Once the sources have been fetched, NEOS can be built.
Run the following to build NEOS:
```
cd ~/comma_neos_sdm845
./build.sh sdm845 -c -s 0
```
The `-c` argument to `build.sh` indicates that a clean build should be done, and the `-s 0` argument indicates that ccache should not be used. This will take a while to complete.

## Flashing
Once the build is complete, NEOS can be flashed by rebooting the device into fastboot mode and running the following:
```
OUTPATH=~/comma_neos_sdm845/out/target/product/sdm845
fastboot flash boot $OUTPATH/boot.img
fastboot flash dtbo $OUTPATH/dtbo.img
fastboot flash system $OUTPATH/system.img
fastboot flash vbmeta $OUTPATH/vbmeta.img --disable-verity
fastboot flash vendor $OUTPATH/vendor.img
```
After that completes, run `fastboot reboot` to reboot into your compiled NEOS image.
