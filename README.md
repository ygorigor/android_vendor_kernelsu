# KernelSU-Next (LKM)

Loads KernelSU-Next as a kernel module on the stock signed GKI, without
touching boot or init_boot:

1. `rdinit=/init.ksu` on the vendor_boot cmdline makes the kernel run
   `/init.ksu` instead of `/init`.
2. `/init.ksu` is upstream `ksuinit` with
   `ksuinit/0001-ksuinit-Support-starting-via-rdinit.patch`. It loads
   `/kernelsu.ko` and then execs the untouched first stage `/init`.

Both files are installed to the vendor ramdisk root. The manager app is not
bundled: install the official KernelSU-Next APK.

| File | Source |
|---|---|
| `prebuilt/kernelsu.ko` | v3.4.2 `aarch64_android14-6.1_kernelsu.ko`, sha256 `961d2ef0e135a71d2620f10ebdc6932ff5b43069c5cf7da595fba5ab666c4b72` |
| `prebuilt/init.ksu` | v3.4.2 (`4c706b59`) `userspace/ksuinit` + patch, NDK r29, sha256 `3246e99d73498ff281d5b0957410105486586e423541fae5e0cf87b9c0f058d3` |

Update with `./update.sh <tag> <ndk dir> [kmi]`. The KMI defaults to
`android14-6.1`; pass e.g. `android16-6.12` after a kernel upgrade.

Licenses: `kernelsu.ko` is GPL-2.0-only (`LICENSE.GPL-2.0`), `ksuinit` is
GPL-3.0 (`LICENSE.GPL-3.0`).
