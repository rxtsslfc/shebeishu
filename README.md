# TWRP Device configuration for Motorola Edge 30 Fusion

The Motorola Edge 30 Fusion (codenamed _"tundra"_) are high-end smartphones from Motorola.

## Device specifications

| Feature                 | Specification
| :---------------------- | :--------------------------------
| Chipset                 | Qualcomm SM8350 Snapdragon 888+ 5G (5 nm)
| CPU                     | Octa-core (1x2.99 GHz Cortex-X1 & 3x2.42 GHz Cortex-A78 & 4x1.80 GHz Cortex-A55)
| GPU                     | Adreno 660
| Memory                  | 8/12 GB LPDDR5
| Shipped Android Version | 12
| Storage                 | 128/256/512 GB (UFS 3.1)
| Battery                 | Li-Po 4400 mAh, non-removable
| Dimensions              | 158.48 x 71.99 x 7.45mm (6.55 inches)
| Display                 | 1080 x 2400 pixels, AMOLED, 1B colors, 144Hz, HDR10+, 1100 nits (HBM)
| Rear Camera             | 50 MP, f/1.8, (wide), 1/1.55", 1.0µm, multi-directional PDAF, OIS
|                         | 13 MP, f/2.2, 120˚ (ultrawide), 1.12µm, AF
|                         | 2 MP, f/2.4, (depth)
| Front Camera            | 32 MP, f/2.5, (wide), 1/2.8", 0.8µm, AF
| Extras                  | Stereo Speakers, NFC, Bluetooth 5.2 A2DP LE, Wi-Fi 802.11 a/b/g/n/ac/6e, USB Type-C 3.1, Charging 68W wired
| Sensors	          | Fingerprint (under display, optical), accelerometer, gyro, proximity, compass
| Touch Sampling Rate     | 360 Hz
| Release Date            | 2022, September 08

## Device picture

![Device Picture](https://pbs.twimg.com/media/Fb6M8A8aUAATmmE.jpg)

## Kernel

Prebuilt kernel from stock ROM user 11 S3SJ32.1-86-2 3d4dd3 release-keys

## Compile

First repo init the twrp-12.1 tree (and necessary qcom dependencies):

```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorla_tundra" path="device/motorola/tundra" remote="TeamWin" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/5445

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_tundra-eng
make adbd bootimage
```
