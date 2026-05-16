# Prusa CORE One – HT450 Firmware (PT1000 / 450 °C)

![Cover](https://github.com/user-attachments/assets/cd055461-2190-4792-8008-bf42d5a332fd)

This repository is a **fork** of **Prusa Research – Prusa-Firmware-Buddy** with additional changes for the **Prusa CORE One** to enable **high-temperature operation (up to 450 °C)** and to keep the build reproducible.

> ⚠️ **Safety disclaimer**
>
> High-temperature printing can damage hardware and can be hazardous if done incorrectly (overheating, connector damage, wiring insulation failure, fire risk).
> You are responsible for validating your full hardware setup (heater, wiring, connectors, fuses/PSU, sensor wiring, thermal runaway protection, airflow).
> This firmware is provided **as-is**, without warranty. Use at your own risk.

---

## What this fork changes (high level)

- Enables/extends the nozzle temperature range for **CORE One** to **0–450 °C** (intended for PT1000-based setups).
- Integrates and aligns upstream code required to build cleanly (CMake/Marlin sync).
- Includes multiple **build fixes** discovered during integration (missing sources, link fixes, include paths).
- Keeps the project buildable using `utils/build.py` (toolchain auto-download).

> Note: If you flash this firmware while still using the **original hotend sensor** (not PT1000), temperature readings may be inaccurate and/or safety logic may not behave as expected. Only proceed if you understand the consequences and have verified the sensor chain.

---

## Credits / Acknowledgements

- **Upstream (Prusa Research):** https://github.com/prusa3d/Prusa-Firmware-Buddy  
- **High-temp groundwork (metacollin):** https://github.com/metacollin/Prusa-Firmware-Buddy  

This repo builds on the above work. My contributions are primarily the **CORE One HT450 adjustments** and the **integration/build fixes** required to produce working binaries.

---

## Important: Version suffix and PrusaSlicer / Prusa Connect “print host” issues

- Some setups validate the printer firmware “version string” when sending jobs.  
- If the suffix format is unexpected, you may get **print host / upload / send-to-printer errors**.

![Fehlermeldung](https://github.com/user-attachments/assets/345394b0-c230-4b4c-9e30-fc70c107f82a)


✅ Recommendation: build with a suffix that includes a `+<digits>` prefix (then optionally `.HT450`), e.g.:

- `+2636.HT450`
- `+10523.HT450`

---

# Build (Windows / Linux)

## From repo root:
- py utils/build.py --preset coreone --build-type release --version-suffix "+2636.HT450"

## Build outputs are usually under:

- build/coreone_release_boot/
- build/coreone_release_noboot/

## Look for a file named similar to:

- firmware.bbf

---
# Flash Firmware

## Unsigned firmware / flashing note

- By default, developer builds may be unsigned (depending on your build configuration).
- Many devices require enabling developer/service procedures (and sometimes breaking a seal) before accepting unsigned firmware.
- Proceed only if you understand the implications.

![Siegel](https://github.com/user-attachments/assets/2333b634-ed8b-4fc4-82ad-481ec49b7819)


## Which binary should I flash? (boot vs noboot)

- I was only able to successfully flash the modified firmware with the “boot” version.
- In practice, flashing depends on your device state and constraints (e.g., service/dev mode, seal, signing).
- If you are unsure: start with noboot.
- You must confirm the unsigned firmware with “ignore” using the side dial.

![Ignore](https://github.com/user-attachments/assets/1e54020e-2029-4d04-a9fb-67006b91533a)
  
---
# IMPORTANT

## License

- This repository follows the upstream licensing of Prusa-Firmware-Buddy.
- See the upstream LICENSE file(s) and all included third-party notices.
- Nothing here overrides upstream license terms.

## Support / Issues

If you open issues, please include:
- Exact printer model (CORE One)
- Your firmware version string (shown in menu)
- Whether you flashed boot or noboot
- Whether you use PT1000 (and how it’s wired)
- Full build log snippet around the error (if build-related)
