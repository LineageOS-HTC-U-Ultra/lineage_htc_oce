# LineageOS 21 for HTC U Ultra (oce)

Unofficial LineageOS 21.0 / Android 14 build configuration for the HTC U Ultra.
This repository provides the local manifest used to sync the device-specific
source and links to ROM builds published on GitHub Releases.

- **Device:** HTC U Ultra
- **Codename:** `oce`
- **Android base:** Android 14 (LineageOS 21.0)
- **Manifest:** [`lineage-21.0.xml`](lineage-21.0.xml)
- **ROM downloads:** [GitHub Releases](https://github.com/LineageOS-HTC-U-Ultra/lineage_htc_oce/releases)

## Build

Prepare a supported Linux build host and install the packages required by the
[LineageOS build guide](https://wiki.lineageos.org/build/). Initialize the
LineageOS 21.0 source tree, add this repository's local manifest, then sync:

```sh
repo init -u https://github.com/LineageOS/android.git -b lineage-21.0
mkdir -p .repo/local_manifests
curl -fsSL \
  https://raw.githubusercontent.com/LineageOS-HTC-U-Ultra/lineage_htc_oce/main/lineage-21.0.xml \
  -o .repo/local_manifests/oce.xml
repo sync -c
```

Build the `oce` userdebug target:

```sh
source build/envsetup.sh
lunch lineage_oce-ap2a-userdebug
m bacon
```

The resulting ROM package is written under `out/target/product/oce/`.

## What the manifest syncs

The manifest adds the device tree, kernel, and proprietary vendor tree, and
uses the HTC U Ultra org's LineageOS 21.0 forks for projects with device
changes. In particular, the vendor repository supplies `vendor/htc/oce`, so
extracting proprietary files separately is not required for this build setup.

It also pins `external/connectivity` to a specific LineageOS commit needed by
the device configuration. The manifest lists all project names, checkout
paths, branches, and that pinned revision.

## ROM releases

ROM ZIP files are published under [Releases](https://github.com/LineageOS-HTC-U-Ultra/lineage_htc_oce/releases),
not stored in Git. Read the notes for the specific release before installing;
they contain the build details and any release-specific instructions.

When reporting a problem, include the release tag, device codename (`oce`),
whether the issue reproduces on a clean install, and relevant logs.
