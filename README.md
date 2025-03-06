# Snapserver Setup Files

Documentation for the Snapcast and Home Assistant configuration.

## Network Information
- **Home Assistant:** 192.168.178.82:8123
- **Snapweb (volume/zone controls):** 192.168.178.82:1780
- **Snapkitchen Client:** snapkitchen.local

## SSH Access
### Main Server
ssh snapcast@192.168.178.82
Username: snapcast

### Kitchen Client
ssh snapkitchen@192.168.178.83
Username: snapkitchen

## System Configuration
The main server runs:
- Default Pi OS
- Librespot
- Snapcast server
- Snapcast client (for central Spotify control)
- Home Assistant (Docker container)

## Configuration Files
sudo nano /etc/snapserver.conf
sudo nano /etc/systemd/system/librespot.service
sudo nano /etc/systemd/system/librespot-amy.service
sudo nano /etc/systemd/system/librespot-peter.service
sudo nano /etc/systemd/system/librespot-guest.service
sudo nano /etc/systemd/system/snapserver.service
sudo nano /etc/systemd/system/snapclient-zone1.service
sudo nano /etc/systemd/system/snapclient-zone2.service
sudo nano /etc/systemd/system/snapclient-zone3.service
sudo nano /etc/systemd/system/snapclient-zone4.service

## Adding New Zones
For new Behringer UAC202 units (ie new zone connected using usb):
1. Connect new UAC202
2. Run `aplay -l` to get its card number
3. Create a new service file (e.g., `snapclient-zone4.service`)
4. Update the `-s` parameter with the new card number
5. Update the `hostID` for the new zone

Use `snapclient-zone1.service` as a blueprint for new zones.

## Troubleshooting
Run `sudo systemctl restart librespot-name.service` or `sudo systemctl status librespot-name.service` if services stop after power cuts.
