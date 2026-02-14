# Brief introduction for using MediaTek released OpenWrt SDK

## 1. Build system setup

- Please refer to https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem

## 2. Clone vanilla OpenWrt

Currently one release branches are supported:

1. 24.10
    This is the current in-use branch

   ```bash
   git clone -b openwrt-24.10 https://git.openwrt.org/openwrt/openwrt.git
   ```

## 3. Add MediaTek OpenWrt feed

```bash
cd openwrt
echo "src-git mtk_openwrt_feed https://github.com/db260179/mtk-openwrt-feeds.git;24.10" >> feeds.conf.default
./scripts/feeds update -a
./scripts/feeds install -a
```

## 4. Apply MediaTek OpenWrt files and patches

1. 24.10 branch

   ```bash
   cp -af ./feeds/mtk_openwrt_feed/24.10/files/* .
   for file in $(find ./feeds/mtk_openwrt_feed/24.10/patches-base -name "*.patch" | sort); do patch -f -p1 -i ${file}; done
   ```

## 5. Configuration

```bash
make menuconfig
```

1. 24.10 branch

   ```text
   Target System -> MediaTek Ralink ARM
   Subtarget -> Filogic 8x0 (MT798x)
   Target Profile -> select as needed
   ```

## 6. Build

```bash
make V=s -j$(nproc)
```

# Mediatek Official Release with autobuild framework
1. OpenWrt24.10 branch: [Kernel6.6 Release](https://git01.mediatek.com/plugins/gitiles/openwrt/feeds/mtk-openwrt-feeds/+/refs/heads/master/autobuild/unified/Readme.md)

