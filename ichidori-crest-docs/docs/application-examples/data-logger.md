# GNSS Data Logger

Log GNSS data locally on the Raspberry Pi while streaming corrections via LTE.

## Basic NMEA Logging

```bash
# Log NMEA from mosaic-G5 COM1 to file, timestamped
while true; do
    cat /dev/ttyAMA0 >> /home/pi/gnss-log-$(date +%Y%m%d).nmea
done
```

## Log with Rotation (logrotate)

Create `/etc/logrotate.d/gnss`:

```
/home/pi/gnss-log-*.nmea {
    daily
    rotate 7
    compress
    missingok
    notifempty
}
```

## SBF Binary Logging (mosaic-G5)

mosaic-G5 supports Septentrio Binary Format (SBF) for compact, precise logging.

Configure via mosaic-G5 web interface or COM1:

```
# Enable SBF output on COM1
setSBFOutput, COM1, PVTGeodetic+MeasEpoch, sec1
```

Then log:

```bash
cat /dev/ttyAMA0 > /home/pi/gnss-$(date +%Y%m%d-%H%M%S).sbf &
```

## Systemd Service for Continuous Logging

```ini
# /etc/systemd/system/gnss-logger.service
[Unit]
Description=GNSS Data Logger
After=multi-user.target

[Service]
ExecStart=/bin/bash -c 'cat /dev/ttyAMA0 >> /home/pi/gnss-$(date +%%Y%%m%%d).nmea'
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable gnss-logger
sudo systemctl start gnss-logger
```
