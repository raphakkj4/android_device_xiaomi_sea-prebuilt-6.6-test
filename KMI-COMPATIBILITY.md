# Kernel and module compatibility

The `kernel`, DT images, and loadable modules in this branch are one matched
Android 15 6.6 KMI set. Do not replace only the kernel image while keeping the
prebuilt modules.

The expected module ABI can be checked with:

```sh
modprobe --dump-modversions vendor_ramdisk/bootprof.ko |
    grep module_layout
```

The expected `module_layout` CRC is `0x4e276f37`.

The included compressed kernel identifies itself as:

```text
6.6.58-android15-8-g19e0e8cef6b2-4k
```

If a locally built kernel exports a different `module_layout` CRC, rebuild all
vendor modules against that kernel or restore KMI compatibility. Bypassing the
kernel module version checks is unsafe because an incompatible module can
corrupt memory during early boot.
