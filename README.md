# Android manifest for Comma Tici 
## Base source
Pulled from https://source.codeaurora.org/quic/la/platform/manifest/plain/LA.UM.6.3.r7-01900-sdm845.0.xml?h=LA.UM.6.3.r7-01900-sdm845.0

## Build instructions
* Initialize repo: `repo init -u https://github.com/commaai/android/ -b tici-8`
* Sync repo: `repo sync`
* Run `./build.sh tici -j$(nproc)`
* Profit
