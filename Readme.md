# OpenAmbient

**Open-source, privacy-preserving ambient environmental data collection and monitoring for clinical research.**

OpenAmbient is a complete platform (hardware, firmware, and self-hosted software) for collecting objective environmental data in hospitals, clinics, and other settings where instrumentation has historically been the primary barrier to research progress.

---

## Why OpenAmbient?

Clinical researchers studying the relationship between the clinical environment and patient outcomes face a persistent problem: collecting reliable, continuous environmental data in healthcare settings is expensive, technically complex, and logistically burdensome. Studies have been stalled by denied network access, improvised workflows, undetected power outages, incomplete records, and multi-year timelines - often to measure a single parameter.

OpenAmbient exists to make objective environmental measurement accessible, standardized, and reproducible.

## What It Measures

OpenAmbient can continuously monitors five physical environmental parameters:

- **Light** — Spectral power distribution, correlated color temperature (CCT), melanopic equivalent daylight illuminance (m-EDI), lux, and flicker detection
- **Sound** — Frequency-weighted sound pressure levels (dBA and dBC), equivalent continuous levels, and peak metrics
- **Temperature** — Sub-0.01°C resolution
- **Humidity** — Relative humidity with cross-sensor compensation
- **Air Quality** — Total volatile organic compounds (TVOC) in ppb, equivalent CO₂ in ppm, and particulate matter mass and number concentration across independently measured size bins (PM1.0, PM2.5, PM4.0, PM10)

Additional contextual data includes passive infrared motion/occupancy detection and accelerometer-based tamper logging.

All measurements are reported in established SI units.

## Design Philosophy

| Principle | Description |
|---|---|
| **Open source, end to end** | Schematics, PCB layout, firmware, and data platform are all publicly available. No vendor lock-in or licensing fees. |
| **Research-grade accuracy, accessible pricing** | Sensor selection prioritizes metrological performance at the lowest possible cost. |
| **Privacy-preserving** | No cameras, no speech recording, no patient identifiers. Sound is processed entirely on-device. All data is area-level by design. |
| **Infrastructure-independent** | Cellular connectivity (LTE-M / NB-IoT) eliminates the need for hospital Wi-Fi or IT approvals. |
| **Uninterrupted operation** | Integrated backup battery maintains data collection during power outages with remote alerting. |
| **Modular by design** | Every sensor can be independently excluded at assembly time. Tailor each board to your study; reduce cost and complexity without a redesign. |
| **Regulatory-ready** | All RF-emitting modules carry pre-certified FCC/IC approvals. |
| **Reusable** | Devices can be wiped, reconfigured, and redeployed across studies and institutions. |

## System Architecture

Deployed devices transmit environmental data to your self-hosted OpenAmbient platform via LTE-M/NB-IoT cellular connectivity. The platform provides:

- **Remote device management** — Configure sensors, sampling intervals, and connectivity settings from a web dashboard
- **Real-time monitoring** — Live telemetry confirms each device is collecting and transmitting as expected
- **Over-the-air updates** — Push firmware and configuration changes without visiting each device
- **Data export** — Download datasets in standardized formats for analysis
- **Alerting** — Get notified if a device loses power or goes offline

Local SD card logging on each device ensures complete data continuity in the event of transient connectivity loss.

## Getting Started

### 1. Order Hardware

Download production files (Gerber files, bill of materials, and pick-and-place data) from this repository and upload them to a PCB fabricator such as [JLCPCB](https://jlcpcb.com). The fabricator handles component sourcing and surface-mount assembly. Enclosure files for 3D printing (SLA recommended) are included.

**No electrical engineering or soldering expertise is required.**

Only populate the sensors you need — the modular design lets you reduce per-unit cost by leaving unused sensor footprints unpopulated.

### 2. Provision the Platform

Deploy the self-hosted OpenAmbient platform on a cloud instance (e.g., a DigitalOcean Droplet starting at ~$4 USD/month). The guided setup handles database initialization and dashboard configuration.

### 3. Activate Connectivity

Each device requires a commercial IoT SIM card (typically < $2/month from providers such as [Hologram](https://hologram.io) or [Soracom](https://soracom.io)). Configure APN credentials through the dashboard.

### 4. Configure and Deploy

Select which parameters each device should collect and set your desired sampling interval through the dashboard. Provision devices over USB, place them in your target environment, and plug into a standard wall outlet. Devices begin transmitting within minutes.

### 5. Collect and Export Data

Monitor your fleet remotely throughout your study. Export data from the dashboard or retrieve it from each device's onboard SD card. When the study concludes, wipe and redeploy devices for your next project.

## Cost

Total bill of materials is approximately **$100–130 USD per device** at modest quantities, with the particulate matter sensor representing roughly 30% of the total. Omitting sensors you don't need reduces cost proportionally. Recurring costs are limited to a shared cloud instance and an IoT SIM per device — on the order of a few dollars per month.

## Repository Structure

```
├── hardware/          # Schematics, PCB layout, Gerber files, BOM, pick-and-place
├── enclosure/         # 3D-printable enclosure design files
├── firmware/          # ESP-IDF based device firmware
├── platform/          # Self-hosted data platform (backend + dashboard)
└── docs/              # Documentation, deployment guides, calibration procedures
```

## Contributing

OpenAmbient is built for the research community. Contributions are welcome.

## License

OpenAmbient uses a dual-license structure to provide appropriate legal coverage across hardware and software:

| Component | License | File |
|---|---|---|
| Hardware (schematics, PCB layout, BOM, Gerbers) | [CERN Open Hardware Licence v2 — Strongly Reciprocal](https://ohwr.org/cern_ohl_s_v2.txt) | [LICENSE-HARDWARE](LICENSE-HARDWARE) |
| Enclosure (3D-printable design files) | [CERN Open Hardware Licence v2 — Strongly Reciprocal](https://ohwr.org/cern_ohl_s_v2.txt) | [LICENSE-HARDWARE](LICENSE-HARDWARE) |
| Firmware | [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.txt) | [LICENSE](LICENSE) |
| Platform software | [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.txt) | [LICENSE](LICENSE) |
| Documentation | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) | — |

Both CERN-OHL-S and GPLv3 are strongly reciprocal — if you modify and distribute OpenAmbient, you must share your changes under the same terms. You are free to use, modify, manufacture, and sell OpenAmbient, provided modified designs and source code remain open.
