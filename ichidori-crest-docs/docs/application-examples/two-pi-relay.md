# Two-Pi Relay

Use two Raspberry Pi units: one in the field with iChidori-Crest (GNSS + LTE), one in the office as an NTRIP caster or relay server.

## Architecture

```
[Field Pi]                    [Office Pi / VPS]
iChidori-Crest                NTRIP Caster (str2str)
  mosaic-G5                         ↑
     ↓ NMEA/SBF                RTCM relay
  str2str                           ↑
     ↓ NTRIP push           [RTK Client (rover)]
  LTE (ppp0)
     ↓ internet (Tailscale)
  [Office Pi]
```

## Field Pi: Push GNSS Stream

```bash
str2str \
  -in serial://ttyAMA0:115200 \
  -out ntrip://user:pass@office-pi:2101/FIELD1
```

## Office Pi: Run NTRIP Caster

Install RTKLIB str2str as caster:

```bash
str2str \
  -in ntrip://user:pass@office-pi:2101/FIELD1 \
  -out ntrips://:2101/RELAY1
```

## Connect via Tailscale

Both Pis are on the same Tailscale network. Use Tailscale IPs:

```bash
str2str \
  -in serial://ttyAMA0:115200 \
  -out ntrip://user:pass@100.64.x.x:2101/FIELD1
```

No port forwarding required — Tailscale handles NAT traversal.
