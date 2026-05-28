# This fork

Personal QMK fork with EVO80 support and GCC 15 / Debian testing compatibility fixes.
Keymaps live separately at [qmk-keymaps](https://github.com/safteinzz/qmk-keymaps).

---

## What's different from mainline

**Added: EVO80 keyboard support**
- `keyboards/evoworks/evo80/` — keyboard files from [carlosedp's fork](https://github.com/carlosedp/qmk_firmware)
- `lib/rdmctmzt_common/` — shared hardware library (wireless modes, RGB, battery)
- `keyboards/evoworks/evo80/evo80.c` — renamed `process_record_user` → `process_record_kb` and `keyboard_post_init_user` → `keyboard_post_init_kb` so keymap callbacks work correctly

**Fixed: GCC 15 + picolibc on Debian testing**
- `lib/chibios-contrib/.../system_fs026.h` — fixed mismatched header guard (`__SYSTEM_ES32F0283_H__` → `__SYSTEM_FS026_H__`)
- `lib/chibios/os/various/syscalls.c` — added `struct _reent;` forward declaration (removed from picolibc)
- `platforms/chibios/platform.mk` — added picolibc auto-detection for ARM targets (falls back to `picolibc.specs` when `nano.specs` is unavailable)

---

## Vendor forks (gitignored)

- `vendor/carlosedp_fork/` — carlosedp's EVO80 fork, reference only
- `vendor/keychron_fork/` — Keychron's official fork, reference only (J4 not in it yet)
