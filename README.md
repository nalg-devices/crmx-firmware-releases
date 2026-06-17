# crmx-firmware-releases

Public distribution channel for **CRMX device firmware binaries**. Built and published
automatically by CI from the private `nalg-devices/CRMXTransceiver` monorepo. Contains
**only built artifacts — no source code**.

The DeviceControl iOS app reads `firmware.json` to compare the device's reported
STM32 / ESP32 firmware versions against the latest available, and downloads the `.bin`
to OTA-flash (over Wi-Fi/USB/Pi-repeater; Bluetooth later).

## Layout
```
firmware.json                      # manifest (see schema below)
stm/<version>/CRMXTransceiver.bin  # STM32H7 image
esp/<version>/crmx_esp.bin         # ESP32 image
```

## firmware.json schema (v1)
- `stm` / `esp`: `{ version, url, sha256, signature, size, notes }`
- `version` is git-derived (tag / `git describe`).
- `sha256` for integrity; `signature` for on-device authenticity verification before
  the bank/slot swap (images are world-downloadable, so authenticity matters).
