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
| `prebuilt/kernelsu.ko` | v3.4.2 `aarch64_android14-5.15_kernelsu.ko`, sha256 `fac9464f54ebca4d1d7fd1ee3a4b8744bcb1965759dc1d7b68346ae9c85c9dd2` |
| `prebuilt/init.ksu` | v3.4.2 (`4c706b59`) `userspace/ksuinit` + patch, NDK r25, sha256 `3fedd8ce0a45858e012dbd7d0191ae2805214ee149a0f46bc3666d7977657431` |

Update with `./update.sh <tag> <ndk dir> [kmi]`. The KMI defaults to
`android14-5.15`; pass e.g. `android16-6.12` after a kernel upgrade.

Licenses: `kernelsu.ko` is GPL-2.0-only (`LICENSE.GPL-2.0`), `ksuinit` is
GPL-3.0 (`LICENSE.GPL-3.0`).
