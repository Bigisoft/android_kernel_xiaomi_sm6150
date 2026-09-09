# Sailfish OS `sweet` port - kernel

Branch `sweet-sailfish` adds only defconfig changes, all of them required by a
hybris port and harmless for Android:

- the eight options `mer-kernel-check` asks for, including
  `USB_CONFIGFS_RNDIS`, which provides the USB networking the whole debug loop
  depends on before the device has a working UI
- `USER_NS` and `PID_NS`, without which sailjail/firejail kills every sandboxed
  application at startup with `clone: Invalid argument` - the visible symptom
  being an app that plays its launch animation and then nothing
- `BT_HCIVHCI` plus `RFCOMM`, `BNEP` and `HIDP`. bluebinder bridges BlueZ to the
  Android Bluetooth HAL through a virtual HCI adapter on `/dev/vhci`; without it
  there is no Bluetooth adapter at all
## The whole port

**Start here:** [droid-config-sweet](https://github.com/Bigisoft/droid-config-sweet) - the device adaptation, and the README that explains the device-specific parts.

| repo | branch | what |
|---|---|---|
| [droid-config-sweet](https://github.com/Bigisoft/droid-config-sweet) | `main` | the device adaptation |
| [droid-hal-version-sweet](https://github.com/Bigisoft/droid-hal-version-sweet) | `main` | version package |
| [droid-hal-sweet](https://github.com/Bigisoft/droid-hal-sweet) | `main` | tree-root `rpm/` spec and the `repo` local manifest |
| [hybris-patches](https://github.com/Bigisoft/hybris-patches/tree/sweet-hybris-23.2) | `sweet-hybris-23.2` | fork - patches an Android 16 base needs |
| [droidmedia](https://github.com/Bigisoft/droidmedia/tree/sweet-android16) | `sweet-android16` | fork - builds against Android 16 |
| [droid-hal-device](https://github.com/Bigisoft/droid-hal-device/tree/sweet) | `sweet` | fork - vendor-side binaries and C++17 helpers |
| [android_kernel_xiaomi_sm6150](https://github.com/Bigisoft/android_kernel_xiaomi_sm6150/tree/sweet-sailfish) | `sweet-sailfish` | fork - defconfig |

Device: Xiaomi Redmi Note 10 Pro (`sweet`), Snapdragon 732G / sm6150, aarch64.
Base: `hybris-23.2` on LineageOS 23.2 (Android 16).