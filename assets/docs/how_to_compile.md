# Step 0:
- Get the build environment ready. For reference, see [here](https://source.android.com/docs/setup/start/initializing).
- Install the required packages for your distro. For reference, see [here](https://source.android.com/setup/build/initializing#installing-required-packages-ubuntu-1804).
- Basics of git. See [here](https://www.atlassian.com/git) for reference.
- Get your device resources ready.
  
# Step 1:
### Initialize the repo and sync the source
```
mkdir fuse && cd fuse
```
```
repo init -u https://github.com/Fusion-OS/manifest -b fourteen
repo sync --current-branch --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune -j$(nproc --all)
```

# Step 2:
### Clone other stuff && bringup device tree

*Assuming you are using LineageOS trees and kernel as base.*

- Clone your device resources to their respective destinations.
- In DT change `lineage` to `fuse` in respective files.
- Inherit `common_full_phone.mk` in your device makefile.
- Remove `LineageOS` specific stuff from your device tree. e.g.: lineagehw, livedisplay, touch etc.

# Step 3:
### Build the source
```
source build/envsetup.sh
lunch fuse_$device-userdebug
make fuse-prod -j$(nproc --all) | tee log.log
```

# Credits:
- [ArrowOS](https://blog.arrowos.net/android/arrowos/guides/compilation-guide/)
- [LineageOS](https://wiki.lineageos.org/devices/bacon/build)