# Specifications

## Mechanical

| Parameter | Value |
|-----------|-------|
| Size | Raspberry Pi HAT (65 × 56 mm) |
| Weight | 25 g |

## Power Supply

| Parameter | Value |
|-----------|-------|
| Input — USB-C | 5V |
| Input — External | 6–24V DC |
| Input — Pi rail | 5V via 40-pin header |

## GNSS — mosaic-G5
The table below summarizes the key differences across the full mosaic-G5 family for reference.

| Feature | P1 | P3 | P3H | P6 |
|---------|----|----|-----|----|
| Frequency Bands | L1/L2/L5 (3-band) | L1/L2/L5/L6 (4-band) | L1/L2/L5/L6 (4-band) | L1/L2/L5/L6 (4-band) |
| Heading Support | — | — | Supported | Supported |
| Update Rate (Position) | 5 Hz | 20 Hz | 20 Hz | 100 Hz |
| Update Rate (RTK + Attitude) | — | — | 20 Hz | 50 Hz |
| Tracking Channels | 789 | 789 | 789 | 789 |
| Interfaces | 2×UART, USB 2.0, GPIO, PPS1/2 | 2×UART, USB 2.0, GPIO, PPS1/2, EVTA/B | 2×UART, USB 2.0, GPIO, PPS1/2, EVTA/B | 2×UART, USB 2.0, GPIO, PPS1/2, EVTA/B |
| Typical Power | 0.44 W | 0.44 W | 0.6 W | 0.44–0.6 W |

=== "mosaic-G5 P1 Features"

    | Item | Specification |
    |------|---------------|
    | **GNSS technology** | |
    | GPS | L1C/A, L1P(Y), L2C, L2P(Y), L5 |
    | GLONASS | L1CA, L2CA, L2P, L3 CDMA |
    | BeiDou | B1I, B1C, B2a, B2I, B3I |
    | Galileo | E1, E5a, E5b |
    | QZSS | L1C/A, L1C/B, L2C, L5 |
    | SDCM | L1, L5 |
    | **Septentrio patented GNSS+ technologies** | 
    | AIM+ anti-jamming, anti-spoofing: essential interference monitoring and mitigation | Basic |
    | **Interfaces** | |
    | USB device | 1 × USB 2.0 (HS) |
    | Event markers | 2 |
    | PPS out | 2 × configurable |
    | **Velocity** | |
    | Velocity accuracy | 3 cm/s |
    | **Maximum update rate** | |
    | Position | 5 Hz |
    | **Package** | |
    | Size | 22.8 x 16.4 x 2.4 mm |
    | Weight | 2.2 g |

=== "mosaic-G5 P6 Features"

    | Item | Specification |
    |------|---------------|
    | **GNSS technology** | |
    | GPS | L1C/A, L1C, L1P(Y), L2C, L2P(Y), L5 |
    | GLONASS | L1CA, L2CA, L2P, L3 CDMA |
    | BeiDou | B1I, B1C, B2a, B2I, B2b, B3I |
    | Galileo | E1, E5a, E5b, E6 |
    | QZSS | L1C/A, L1C/B, L2C, L5, L6 |
    | NavIC | L5 |
    | SBAS | EGNOS, WAAS, GAGAN, MSAS |
    | GNSS heading |
    | Galileo High Accuracy Service (HAS) |
    | Galileo OSNMA |
    | Full Raw measurements data|
    | 4-constellation (rover) |
    | **Septentrio patented GNSS+ technologies** | 
    | AIM+ anti-jamming, anti-spoofing Interference Monitoring and Mitigation | Premium |
    | **Interfaces** | |
    | USB device | 1 × USB 2.0 (HS) |
    | Event markers | 2 |
    | PPS out | 1 × configurable |
    | **Positioning modes accuracy** | |
    | Horizontal RTK | 0.6 cm |
    | Vertical RTK | 1 cm |
    | Horizontal Galileo HAS | 0.1 m |
    | Vertical Galileo HAS | 0.2 m |
    | **GNSS attitude accuracy** | |
    | Heading (antenna separation 1 m) | 0.15° |
    | Pitch/Roll (antenna separation 1 m) | 0.25° |
    | Heading (antenna separation 5 m) | 0.03° |
    | Pitch/Roll (antenna separation 5 m) | 0.05° |
    | **Maximum update rate** | |
    | Position | 100 Hz |
    | RTK + Altitude | 50 Hz |
    | **Package** | |
    | Size | 22.8 x 16.4 x 2.4 mm |
    | Weight | 2.2 g |


<div markdown style="display: flex; justify-content: space-between;">

**Back:** [← Interfaces](interfaces.md)

**Next:** [Getting Started →](../getting-started/basic-setup.md)

</div>

---

## Quick Navigation

<div class="grid cards" markdown>

- :material-home: **[Home](../index.md)**  
  Welcome and project overview

- :material-play-circle: **[Getting Started](../getting-started/basic-setup.md)**  
  Step-by-step setup from unboxing to first fix

- :material-antenna: **[Application Examples](../application-examples/clas-madoca.md)**  
  RTK, data logger, RxTool experiments

- :material-wrench: **[Troubleshooting](../troubleshooting.md)**  
  Common issues and fixes

</div>