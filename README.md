# [Help Needed] HTC U19e (2Q7A100 / htc_tetdugl) - Unbrick / Full Stock Dump Request

### Device Specifications
- **Device Model:** HTC U19e (Model ID: `2Q7A100` / Product Codename: `htc_tetdugl`)
- **SoC / Chipset:** Qualcomm Snapdragon 710 (`SDM710`)
- **Region / CID:** Taiwan (`HTC__039` / `HTC__621`, Software build: `1.00.709.x`)
- **Android OS:** Android 9.0 (Pie) with HTC Sense
- **Stock Fingerprint:** `htc/htc_tetdugl_00709/htc_tetdugl:9/PKQ1.181030.001/200619`

---

### Current Problem & Status
The phone is currently soft-bricked and stuck in a bootloop. **Fastboot**, **Stock Recovery**, and **Qualcomm EDL 9008** modes are fully functional, but it cannot boot into Android OS.

1. **Bootloader Status:** `*** LOCKED ***` (`unlocked: no`)
2. **Fastboot Failure:** Because the OS cannot boot, **"OEM Unlocking"** could not be toggled in Developer Options. Executing `fastboot flashing unlock` fails with:
   ```text
   FAILED (remote: 'Flashing Unlock is not allowed')
   ```
3. **Recovery Sideload Failure:** Official incremental OTA patches (`OTA_1.00.709.28-1.00.709.300d96mg614cdk074q.zip`) retrieved directly from `fotadl.htc.com` abort installation (`Installation aborted`) because the existing system partition hash does not match due to corruption.

---

### Hardware Diagnostics & EDL 9008 Handshake Data
The phone successfully enters **Qualcomm Emergency Download Mode (EDL 9008)** (`VID: 05C6, PID: 9008`).
Through the Sahara protocol handshake with `bkerler/edl`, the device returned the following hardware identifiers:

```text
HWID:       0x000db0e106360666 (MSM_ID: 0x000db0e1, OEM_ID: 0x0636, MODEL_ID: 0x0666)
CPU:        SDM710
PK_HASH:    0x9684c7577746f6333fb45e2dccb2052a4e2679dd69eee3989a7e359b8b4c0379
```
*Note: Generic SDM710 firehose programmers fail authentication because the OEM public key hash (PK_HASH) is enforced by Qualcomm SecureBoot.*

---

### How You Can Help (Files Needed)
If you own a working **HTC U19e** or have access to archived HTC engineering files, any of the following files would help resurrect this device:

1. **Raw Partition Dumps (from a working device via root/dd):**
   - `boot.img` (~64 MB)
   - `system.img` (~4 GB)
   - `vendor.img` (~1 GB)
   - `vbmeta.img`
2. **Official Full RUU / `2Q7AIMG.zip`** (Non-incremental full package).
3. **Signed Qualcomm Firehose Programmer** for this specific PK_HASH:
   - `000db0e106360666_9684c7577746f633_fhprg.bin` (or `.elf`).

---

### 中文求助說明（徵求台灣 HTC U19e 同好備份）
我的 HTC U19e 目前系統損毀無法開機，Bootloader 處於 LOCKED 狀態，因進不去系統開啟「OEM 解鎖」開關，Fastboot 無法放行解鎖指令。原廠 Recovery 僅支援未損毀分區的差分更新，推入增量 OTA 包會被 aborted。

目前設備硬體完好，可進入 Fastboot、Recovery Sideload 以及高通 9008 深度刷機模式。若有手邊持有正常運作 HTC U19e 的同好，懇請協助透過 Root/dd 備份出原廠未修改的 `boot.img`、`system.img` 或完整映像檔，萬分感激！

---
*Created by [windows64](https://github.com/windows64)*