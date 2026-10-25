# Configuring mosaic-G5 as an RTK Rover

### Overview

 In this article, we use the built-in **NTRIP Forwarder** in RxControl to stream RTCM3 correction data directly to the receiver and achieve an RTK Fixed solution.

---

### Setup Requirements

- iChidori-Crest connected to PC via USB-C cable
- RxControl connection established (see [Basic Setup](basic-setup.md))
- Active NTRIP caster credentials and mountpoint
- Ensure that a GNSS antenna (or two, for Dual Antenna mode) connected to iChidori-Crest and placed antenna in open sky view

---

### Open the NTRIP Forwarder in RxControl

With the iChidori-Crest connected in RxControl, navigate to the RXControl NTRIP Forwarder:

Open **Communication → RXControl NTRIP Forwarder**. Click **Edit**:

Enter NTRIP caster details:

| Field | Value |
|---|---|
| Caster | ntrip.aitoya.net |
| Port | 2101 |
| Mountpoint | MOSAIC-RTCM3 |

Click **Connect** to begin streaming correction data to the receiver.

<!-- Screenshot: RxControl NTRIP forwarder settings -->

---

### Verify RTK Fixed

Once corrections are streaming, monitor the receiver status in RxControl. The position mode indicator will transition through the following states:

| Status | Description |
|---|---|
| No Fix | No GNSS solution |
| Standalone | GNSS fix, no corrections |
| DGPS | Differential correction applied |
| RTK Float | Corrections received, ambiguity not resolved |
| **RTK Fixed** | **Full RTK solution — centimeter-level accuracy** ✓ |

<!-- Screenshot: RxControl showing RTK Fixed status -->

Wait for the status to reach **RTK Fixed** before proceeding.

---

### Summary

In this test, we used the built-in NTRIP forwarder in RxControl to stream RTCM3 correction data to the mosaic-G5 and confirmed an RTK Fixed solution. This is the quickest way to verify rover operation directly from a PC.

!!! tip
    RxControl's NTRIP forwarder is convenient for quick evaluation. For TCP/IP-based correction streaming or more advanced data link configurations, use the **Data Link Tool** included in RxTools.

In the next test, we will log receiver data and evaluate positioning performance in detail using the **SBF Analyzer Tool**.



**Next:** [Data Logging →](sd-logging.md)