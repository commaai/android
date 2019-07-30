# Android manifest for Comma Tici 
## Base source
This manifest is based on the latest Android 9 release, modified by Code Aurora Forum to support the Qualcomm SDM845. Cloned tag is `LA.UM.7.3.r1-07900-sdm845.0`.

## Build instructions
* Initialize repo: `repo init -u https://github.com/commaai/android/ -b tici`
* Sync repo: `repo sync`
* Run `./build.sh tici -j$(nproc)`
* Profit
