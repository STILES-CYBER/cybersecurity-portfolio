# Ubuntu Kernel Panic — Missing Initramfs Recovery

**Environment:** HP EliteBook 830 G6, Ubuntu/Windows dual-boot, internal SSD
**Date:** July 2026

## Summary

Normal boot into Ubuntu failed with a kernel panic, while GRUB's recovery mode
booted successfully. Root cause was a missing/corrupted initramfs image for
the newest installed kernel. Fixed by rebuilding the initramfs for that
specific kernel version and refreshing GRUB — no data loss, no reinstall.

## Symptom

On boot, the screen displayed:

```
KERNEL PANIC!
VFS: Unable to mount root fs on unknown-block(0,0)
Please reboot your computer.
```

Normal boot failed consistently. GRUB's **Advanced options → recovery mode**
booted without issue.

## Investigation

1. **Ruled out partition loss.** Booted into Windows and checked Disk
   Management — all Linux partitions (EFI, `/boot`, root, swap/reserved) were
   present and marked *Healthy*. This confirmed the disk layout itself was
   intact; the problem was software-level, not a wiped/corrupted partition
   table.

2. **Confirmed the kernel could mount root under the right conditions.**
   Recovery mode reaching a working read-only shell proved the filesystem
   itself was mountable — narrowing the fault to GRUB configuration or a
   kernel-specific initramfs problem rather than disk corruption.

3. **Ran filesystem and bootloader repairs from the recovery menu:**
   ```
   fsck            # Check all filesystems — came back clean
   update-grub     # Regenerate /boot/grub/grub.cfg
   ```
   This alone got the system booting again — but only into the **older**
   kernel (`6.17.0-35-generic`). The newest kernel (`7.0.0-28-generic`),
   which GRUB defaults to, still panicked on a normal boot.

4. **Identified the specific broken kernel.** GRUB's menu listed multiple
   kernel versions:
   ```
   Ubuntu with Linux 7.0.0-28-generic          <- default, broken
   Ubuntu with Linux 6.17.0-35-generic         <- working
   ```
   This is a classic sign of an interrupted or incomplete kernel update: the
   newest kernel's package files exist, but its initramfs was never built or
   got corrupted.

5. **Rebuilt initramfs for all kernels:**
   ```bash
   sudo update-initramfs -u -k all
   ```
   Confirmed normal boot worked afterward for a session, but the issue
   recurred — the specific broken kernel needed its initramfs rebuilt from
   scratch (`-c` = create) rather than updated (`-u`).

## Root Cause

Kernel `7.0.0-28-generic` had no valid initramfs image on disk. `update-grub`
was pointing the default boot entry at this kernel, so the bootloader handed
off to a kernel that had no early-boot image to mount root — hence the
`unknown-block(0,0)` panic. `apt --reinstall` was attempted first but failed
because the kernel package wasn't resolvable via `apt-cache` in the moment,
likely due to a stale package cache.

## Fix

From a normal boot on the working kernel:

```bash
sudo update-initramfs -c -k 7.0.0-28-generic   # (c)reate, not update — image was missing, not stale
sudo update-grub
sudo reboot
```

Confirmed: system now boots cleanly into `7.0.0-28-generic` by default.

## Lessons / Notes for future reference

- **Recovery mode booting ≠ system is fine.** It often boots an older,
  known-good kernel by default, which can mask a broken newest-kernel
  install if you don't check GRUB's kernel list closely.
- **`update-initramfs -u` vs `-c`:** `-u` *updates* an existing initramfs;
  it won't help if the image is missing entirely. `-c` *creates* a fresh one
  for a specific kernel version — the fix here.
- **Windows Disk Management is a useful triage tool** even though it can't
  touch ext4 — confirming partitions are healthy quickly rules out
  disk-level corruption before diving into Linux-side repair.
- **`apt --reinstall` needs an up-to-date package cache** (`apt update`
  first) and only works if the kernel came from a configured repo; a
  missing initramfs doesn't always mean the package itself is broken.
