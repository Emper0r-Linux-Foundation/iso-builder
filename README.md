# iso-builder
Live ISO image generation scripts, bootloaders (GRUB/systemd-boot), and initramfs configs.

## Kernel command line

`boot/cmdline` is the baseline command line managed by the ISO bootloader.
Keep it as the single source of truth for kernel arguments; do not enable
`CONFIG_CMDLINE_OVERRIDE` in the kernel package, so bootloader arguments are
appended rather than replaced.

The baseline enables `mitigations=auto`, the AppArmor/Landlock LSM order,
trusted-boot entropy behavior, module signature enforcement, and the lazy
dynamic-preemption model. Profile-specific options such as `lockdown=integrity`,
`debugfs=off`, and `iommu.strict=1` are intentionally not enabled by default.
