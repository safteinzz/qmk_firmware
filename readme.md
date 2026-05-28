# qmk_firmware — personal fork

Fork of [qmk/qmk_firmware](https://github.com/qmk/qmk_firmware) with support for the **Evoworks EVO80** and fixes for building with GCC 15 and picolibc (which replaced `libnewlib-arm-none-eabi` on some distros).

Keymaps live separately in a userspace repo — see `SAFTEINZZ.md` for the full picture.

---

## Supported (on top of mainline)

| Keyboard | MCU | Notes |
|----------|-----|-------|
| Evoworks EVO80 | ES32 FS026 (Cortex-M0) | ported from [carlosedp/qmk_firmware](https://github.com/carlosedp/qmk_firmware) |

---

## What changed vs mainline

**EVO80 support**
- `keyboards/evoworks/evo80/` — keyboard files
- `lib/rdmctmzt_common/` — shared hardware lib (wireless modes, RGB, battery)
- `keyboards/evoworks/evo80/evo80.c` — fixed callback chain (`process_record_user` → `process_record_kb`, `keyboard_post_init_user` → `keyboard_post_init_kb`)

**GCC 15 compatibility**
- `lib/chibios-contrib/.../system_fs026.h` — fixed mismatched header guard that GCC 15 now errors on
- `lib/chibios/os/various/syscalls.c` — added `struct _reent;` forward declaration, removed in newer picolibc

**picolibc replacing libnewlib-arm-none-eabi**
- `platforms/chibios/platform.mk` — added ARM picolibc auto-detection: falls back to `--specs=picolibc.specs` when `nano.specs` is unavailable and defines `USE_PICOLIBC` so syscall stubs compile correctly

---

## Building

```bash
git clone <this repo> ~/projects/qmk_firmware
cd ~/projects/qmk_firmware
bash util/qmk_install.sh   # needs sudo
qmk setup
qmk compile -kb evoworks/evo80 -km <your_keymap>
```
