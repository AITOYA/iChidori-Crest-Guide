# Connect to a Raspberry Pi

## Overview

So far in this artical series, we have been working with the iChidori-Crest connected to a PC for quick evaluation. In this article, we expand to the **iChidori-Crest + Raspberry Pi**. The iChidori-Crest interfaces with the Raspberry Pi via the 40-pin GPIO header. For pin mapping details, see [40-Pin Header Assignments](../hardware-reference/interfaces.md#40-pin-header-assignments).

We will explore the USB interface of the mosaic G5 module this time. The Pi interfaces with the mosaic-G5 via USB, and we use RTKLIB `str2str` to stream NTRIP corrections to the receiver and try to achieve an RTK Fixed solution. 

![Connect to a Pi  — setup](../images/connect_pi_setup.png){ width="800" }

## Setup Requirement

## Step 1 — Configure mosaic-G5 USB Output

!!! note
    This step configures additional data outputs for post-test debugging and analysis. It is recommended for evaluation purposes.

Open **RxControl** and establish a connection with the mosaic-G5 (see [Basic Setup](../getting-started/basic-setup.md#step-2----connect-rxcontrol-to-the-receiver) if needed).

Navigate to **Communication → Output Settings → NMEA Output** and configure **Stream 1** as follows:

| Field | Value |
|---|---|
| Port | USB1 |
| Message | GGA (or as required)|
| Interval | 1 sec (or as required) |

![NMEA Output — USB1 configuration](../images/usb_nmea_output.png){ width="800" }

Next, navigate to **Communication → Output Settings → SBF Output** and configure **Stream 1** as follows:

| Field | Value |
|---|---|
| Port | USB2 |
| Blocks | PVTGeodetic, MeasEpoch (or as required) |
| Interval | 1 sec (or as required) |

![SBF Output — USB2 configuration](../images/usb_sbf_output.png){ width="800" }

Click **Apply** and **OK** after each setting.

Don't forward to Save to **boot configuration** for the next power cycle.

## Step 2 — Verify mosaic-G5 USB Ports on Raspberry Pi

With the iChidori-Crest HAT attached on Pi and powered, the mosaic-G5 will enumerate two USB serial devices on the Raspberry Pi. These correspond to the USB1 and USB2 ports configured in the previous step.

SSH into the Raspberry Pi and run the following command to confirm both ports are detected:

```bash
ls /dev/ttyACM*
```

If the devices do not appear, check that the USB-C cable between the iChidori-Crest and the Raspberry Pi is connected.

**Verify the USB data stream in the previous setup**

Before proceeding to the next step, confirm that the data is actively streaming from both USB ports on the receiver. Use `str2str` from RTKLIB to read directly from the serial port and print the output to the terminal:

```bash
~/Projects/RTKLIB/app/str2str/gcc/str2str -in serial://ttyACM0:115200 -out -
```

```bash
~/Projects/RTKLIB/app/str2str/gcc/str2str -in serial://ttyACM1:115200 -out -
```

You should see SBF/NMEA sentences scrolling continuously in the terminal like this terminal image:

![NMEA/SBF Output — USB Out Check](../images/usb_out_check.png){ width="800" }

## Step 3 — Forward NTRIP Corrections to mosaic-G5

With the data streams verified on USB ports, we can now stream RTCM3 correction data from an NTRIP caster to the mosaic-G5 receiver via ttyACM0:

```bash
~/Projects/RTKLIB/app/str2str/gcc/str2str \
  -in ntrip://guest:guest@ntrip.aitoya.net:2101/MOSAIC-RTCM3 \
  -out serial://ttyACM0:115200
```

!!! note "Use your own NTRIP caster"
    The example above uses the Aitoya NTRIP caster for reference. Replace the host, port, mountpoint, username and password with your own caster credentials before running.

Once running, `str2str` will continuously receive RTCM3 packets from the caster and forward them to the mosaic-G5 in real time. Leave this process running in the terminal and open a **new terminal window** to proceed to the next step.

![str2str — forwarding NTRIP corrections to mosaic-G5](../images/ntrip_stream.png){ width="800" }

## Step 4 — Verify RTK Fix

With NTRIP corrections streaming to the mosaic-G5, the receiver will begin processing them and improve its position solution - RTK Fixed. Open a new terminal and monitor the NMEA GGA output to track the fix status:

```bash
cat /dev/ttyACM0
```

Watch the fix quality field in the `$GNGGA` sentence (the 6th comma-separated value):

| Fix Quality | Status |
|---|---|
| 0 | No fix |
| 1 | Standalone GNSS fix |
| 2 | DGPS fix |
| 5 | RTK Float — corrections received, ambiguity not yet resolved |
| **4** | **RTK Fixed ✓ — centimeter-level accuracy achieved** |

RTK Fixed GGA output:

![str2str — nmea gga fixed](../images/fix_verify.png){ width="800" }

!!! note
    At this point, the mosaic-G5 is outputting NMEA and SBF data via USB in RTK Fixed state. If you wish to log this data for further evaluation, you can use `str2str` to capture each stream to a file:

    ```bash
    # Log NMEA from ttyACM0
    ~/Projects/RTKLIB/app/str2str/gcc/str2str -in serial://ttyACM0:115200 -out file://<path/to/output>.nma

    # Log SBF from ttyACM1
    ~/Projects/RTKLIB/app/str2str/gcc/str2str -in serial://ttyACM1:115200 -out file://<path/to/output>.sbf
    ```

**Next:** [LTE Connectivity with the iChidori-Crest →](lte-setup.md)
