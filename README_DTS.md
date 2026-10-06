# MikroTik-PatchDTS

MikroTik RouterOS Patch & Keygen (dari `elseif/MikroTikPatch`, versi DTS).

> ⚠️ Testing only. Production = pakai lisensi resmi.

## Alur inti

- `mikro.py` — implementasi kripto MikroTik (KCDSA/EdDSA, software-id encode/decode, encode/decode custom).
- `keygen/` — binary keygen (x86/arm64).
- `npk.py` — create/sign/verify `.npk`.
- `patch.py` — patch key publik bawaan RouterOS → key custom, plus kernel/initrd/netinstall.
- `.github/workflows/` — build pipeline (CI) auto-patch tiap versi baru.
- `option.npk` → pasang dulu, key otomatis highest license + shell.

## Cara kerja "unlimited key"

1. RouterOS sign paket & license pake crypto KCDSA (Curve25519) + EdDSA, key privat di server MikroTik.
2. Repo ganti key **publik** di firmware → key privat punya sendiri (`CUSTOM_LICENSE_PRIVATE_KEY`, `CUSTOM_NPK_SIGN_PRIVATE_KEY`) di GitHub Secrets.
3. `mikro.py` implementasi sign. `keygen/` binary Go — generate key dari software ID, jalan di dalam RouterOS via option.npk shell.
4. Build otomatis (workflow) setiap jam → .npk/ISO/CHR semua dipatch → key auto unlimited.

Jadi "auto unlimited" = ganti trust root di firmware pakai key sendiri, lalu sign semua paket.

## Repo

- Upstream: https://github.com/elseif/MikroTikPatch
- Fork ini: https://github.com/qingzen/MikroTik-PatchDTS
