# mkinitcpio-sd-zfs

A mkinitcpio hook for booting zfs-on-root systems with systemd based initrd

See `help()` in `sd-zfs.initcpio.install` for usage.

## dev notes

- `sd-zfs.initcpio.install` file consumed by mkinitcpio.
- `zfs-root-generator` is the entry point when booting the initrd.
  It reads the cmdline and injects a few systemd units
  and unit overrides that changes the boot process to

  1. import zfs pools
  2. mount the zfs root dataset

  See `systemd.generators(7)` for more information.
- `zfs-set-env` is a helper script that sets the
  environment variable needed by `sysroot.mount`
- `zfs.shutdown` is a simple script that goes in
  `/usr/lib/systemd/system-shutdown/` that is
  executed by `/usr/lib/systemd/system-shutdown`
  on shutdown which exports all zfs pools.
- `parse-cmdline` is a helper awk script that
  parses the kernel command line. Code should be
  pretty self evident with the comments.
