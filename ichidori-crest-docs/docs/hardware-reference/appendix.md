# Appendix A

This appendix provides a technical comparison of the mosaic-G5 variants and selected GNSS receivers.

## A.1 mosaic-G5 Variant Comparison

The following table summarizes the key differences across the mosaic-G5 family.

| Feature | P1 | P3 | P3H | P6 |
|---|---|---|---|---|
| **Frequency Bands** | L1/L2/L5 (3-band) | L1/L2/L5/L6 (4-band) | L1/L2/L5/L6 (4-band) | L1/L2/L5/L6 (4-band) |
| **Heading Support** | — | — | Supported | Supported |
| **Update Rate (Position)** | 5 Hz | 20 Hz | 20 Hz | 100 Hz |
| **Update Rate (RTK + Attitude)** | — | — | 20 Hz | 50 Hz |
| **Tracking Channels** | 789 | 789 | 789 | 789 |
| **GNSS+ Technologies** | Basic | **Premium** | **Premium** | **Premium** |
| **Interfaces** | 2× UART, USB 2.0, GPIO, PPS1/2 | 2× UART, USB 2.0, GPIO, PPS1/2, EVTA/B | 2× UART, USB 2.0, GPIO, PPS1/2, EVTA/B | 2× UART, USB 2.0, GPIO, PPS1/2, EVTA/B |
| **Typical Power** | 0.44 W | 0.44 W | 0.6 W | 0.44–0.6 W |

## A.2 GNSS Receiver Comparison

This section compares the mosaic-G5 P6 with the mosaic-X5 and mosaic-H.

### Signal Bands

| Constellation | mosaic-G5 P6 | mosaic-X5 | mosaic-H |
|---|---|---|---|
| **GPS** | L1C/A, L1C, L2C, L2P, L5 | L1C/A, L1PY, L2C, L2P, L5 | L1, L2 |
| **GLONASS** | L1CA, L2CA, L2P, L3 CDMA | L1CA, L2CA, L2P, L3 CDMA | L1, L2 |
| **Galileo** | E1, E5a, E5b, E6 | E1, E5a, E5b, E5 AltBoc, E6 | E1, E5b |
| **BeiDou** | B1I, B1C, B2a, B2b, B2I, B3I | B1I, B1C, B2a, B2b, B2I, B3 | B1, B2, B3 |
| **QZSS** | L1C/A, L1C/B, L2C, L5, L6 | L1C/A, L1C/B, L2C, L5 | L1C/A, L1C/B, L2 |
| **NavIC** | L5 | L5 | — |
| **SBAS** | — | EGNOS, WAAS, GAGAN, MSAS, SDCM | EGNOS, WAAS, GAGAN, MSAS, SDCM |

### Positioning and Performance

| Feature | mosaic-G5 P6 | mosaic-X5 | mosaic-H |
|---|---|---|---|
| **Horizontal RTK Accuracy** | 0.6 cm + 0.5 ppm | 0.6 cm + 0.5 ppm | 0.6 cm + 0.5 ppm |
| **Vertical RTK Accuracy** | 1 cm + 1 ppm | 1 cm + 1 ppm | 1 cm + 1 ppm |
| **GNSS Channels** | 789 | 448 | 448 |
| **Antenna Configuration** | Single or dual | Single | Dual |
| **Position Update Rate** | 100 Hz | 100 Hz | 100 Hz |
| **RTK + Attitude Update Rate** | 50 Hz | 100 Hz (RTK only)* | 20 Hz |

### Interfaces and Protocols

| Feature | mosaic-G5 P6 | mosaic-X5 | mosaic-H |
|---|---|---|---|
| **UART** | 2 × UART, up to 4 Mbps | 4 × UART, up to 4 Mbps | 4 × UART, up to 4 Mbps |
| **USB** | USB 2.0 HS, 480 Mbps | USB 2.0 HS | USB 2.0 HS |
| **Ethernet** | — | 10/100 Mbps | 10/100 Mbps |
| **SDIO** | — | Mass storage | Mass storage |
| **GPIO** | 2 × GPIO | 2 × GPIO | 2 × GPIO |
| **PPS Output** | 2 × PPS output | 1 × PPS output | 1 × PPS output |
| **Event Markers** | 2 | 2 | 2 |
| **Protocols** | SBF, NMEA, RTCM input | SBF, NMEA, RTCM, CMR | SBF, NMEA, RINEX, RTCM, CMR |

### Physical Specifications and Power

| Feature | mosaic-G5 P6 | mosaic-X5 | mosaic-H |
|---|---|---|---|
| **Size** | 22.8 × 16.4 × 2.4 mm | 31 × 31 × 4 mm | 31 × 31 × 4 mm |
| **Weight** | 2.2 g | 6.8 g | 6.8 g |

---

<div markdown style="display: flex; justify-content: space-between;">

**Back:** [Specifications →](specifications.md)

**Next:** [Getting Started →](../getting-started/basic-setup.md)

</div>