# Mr Smart – iHost Zigbee2MQTT Setup

Installer helper for running Zigbee2MQTT on SONOFF iHost as a prerequisite for the Mr Smart iHost FCU Node-RED integration.

## Tested iHost Docker settings
- Image: `koenkk/zigbee2mqtt`
- Network: `bridge`
- Port: Host `8080` -> Add-on `8080`
- Volume: `zigbee2mqtt-data` -> `/app/data`
- Environment: `ZIGBEE2MQTT_CONFIG_FRONTEND_ENABLED=true`
- USB: select the Zigbee coordinator detected by iHost
- Tested ZBDongle-P add-on path: `/dev/ttyUSB0`

If a newly connected coordinator is not shown and iHost still shows the previous USB device, restart iHost once and reopen the Run screen.

## First-run onboarding
Open `http://<IHOST-IP>:8080`.

Common settings:
- MQTT server: `mqtt://172.17.0.1:1884`
- Base topic: `zigbee2mqtt`
- MQTT version: `4`
- Frontend: enabled, port `8080`
- Home Assistant integration: disabled unless required

### Tested SONOFF ZBDongle-P / CC2652P
- Adapter: `zstack`
- Serial port: `/dev/ttyUSB0`
- Baud rate: `115200`

For other coordinators, select the correct adapter family; do not force `zstack`.

## TYBAC-006 pairing
Enable Permit Join, put the thermostat in Zigbee pairing mode, and wait for a successful interview. Confirm TYBAC-006 / TS0601 and manufacturer `_TZE204_mpbki2zm`. If the first interview fails after joining, re-pair before reinstalling Zigbee2MQTT.

## Mr Smart FCU
After Zigbee2MQTT is operational:
1. Install `node-red-contrib-mrsmart-ihost-fcu`.
2. Configure the iHost connection/token.
3. Configure the installation's MQTT connection.
4. Select/discover the TYBAC-006.
5. Deploy and verify CUBE Web and CAST.

## Automation boundary
The repeatable Zigbee2MQTT settings can be pre-filled or supplied through configuration, but iHost owns host-level USB passthrough in its Docker Run UI. The physical coordinator must therefore be selected/mapped there, and different coordinator families can require different adapter drivers. This package intentionally does not attempt brittle Node-RED-side USB automation.

## Security
Keep MQTT and the Zigbee2MQTT frontend on the trusted local network. Do not expose them publicly without appropriate authentication and transport security.
