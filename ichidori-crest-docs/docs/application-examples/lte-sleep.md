# LTE Sleep Mode

Reduce power consumption by putting the LTE module to sleep when a network connection is not needed.

## GPIO Signals

| Signal | GPIO | Direction |
|--------|------|-----------|
| DTR | GPIO20 | Pi → LTE (HIGH = sleep request) |
| WAKE# | GPIO13 | LTE → Pi (LOW = module awake) |

## Sleep Mode — UART Interface (EC21-J / BG96)

When using UART (not USB), sleep requires two conditions:

1. **AT+QSCLK=1** — enable sleep mode via AT command
2. **DTR HIGH** — assert DTR to signal sleep to module

!!! note "USB not required"
    For UART-only setups, USB suspend is not needed. DTR + AT+QSCLK=1 is sufficient.

## Sleep Test Script

```bash
#!/bin/bash
DTR_PIN=20
WAKE_PIN=13

echo "=== LTE Sleep Mode Test (UART) ==="

# Verify module is responsive before sleep
echo -e "AT\r" > /dev/ttyAMA3
sleep 1
RESPONSE=$(timeout 3 cat /dev/ttyAMA3 2>/dev/null)
echo "Pre-sleep AT response: $RESPONSE"

# Step 1: Enable sleep mode
echo "Step 1: AT+QSCLK=1"
echo -e "AT+QSCLK=1\r" > /dev/ttyAMA3
sleep 2

# Step 2: Assert DTR HIGH → module enters sleep
echo "Step 2: DTR HIGH (sleep request)"
pinctrl set $DTR_PIN op
pinctrl set $DTR_PIN dh

echo "Waiting 5 seconds — measure current now..."
sleep 5

# Verify: AT command should get no response (module asleep)
echo -e "AT\r" > /dev/ttyAMA3
SLEEP_RESPONSE=$(timeout 3 cat /dev/ttyAMA3 2>/dev/null)
if [ -z "$SLEEP_RESPONSE" ]; then
    echo "✓ Sleep confirmed: no AT response"
else
    echo "✗ Module still awake: $SLEEP_RESPONSE"
fi

# Wake: DTR LOW
echo "Step 3: DTR LOW (wake)"
pinctrl set $DTR_PIN dl
sleep 3

# Restore DTR HIGH (idle state after wake)
pinctrl set $DTR_PIN dh

# Verify wake
echo -e "AT\r" > /dev/ttyAMA3
sleep 1
WAKE_RESPONSE=$(timeout 3 cat /dev/ttyAMA3 2>/dev/null)
echo "Post-wake AT response: $WAKE_RESPONSE"
```

Save as `~/lte-sleep-test.sh` and run:

```bash
chmod +x ~/lte-sleep-test.sh
~/lte-sleep-test.sh
```

## BG96 — PSM and eDRX (Cat M1)

BG96 supports Power Saving Mode (PSM) and extended Discontinuous Reception (eDRX), which provide deeper sleep than DTR-based sleep.

!!! warning "Carrier support required"
    PSM and eDRX require network/carrier support. Verify with your carrier before configuring.

### Enable PSM

```
AT+CPSMS=1,,,"00000001","00000001"
```

Timer format (3GPP T3412 / T3324):

- `00000001` = 2 seconds per unit × 1 unit = **2 seconds active timer**
- Adjust per your application duty cycle

### Enable eDRX

```
AT+CEDRXS=2,4,"0010"
```

- Mode 2 = eDRX enabled + report unsolicited result
- AcT-type 4 = LTE-M
- eDRX value `0010` = 20.48 seconds

### Check Current PSM/eDRX Settings

```
AT+CPSMS?
AT+CEDRXS?
AT+CEDRXRDP
```

---

**See also:** [EC21-J Datasheet](../hardware-reference/overview.md), [BG96 AT Commands Manual](#)
