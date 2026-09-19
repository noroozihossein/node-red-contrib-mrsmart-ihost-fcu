# iHost Zigbee2MQTT Installer Checklist

## Recommended – iHost Home Assistant add-on

- [ ] Home Assistant OS is running on iHost.
- [ ] Add repository: `https://github.com/iHost-Open-Source-Project/hassio-ihost-addon`
- [ ] Install **iHost Zigbee2MQTT** from the Add-on/App Store.
- [ ] Ensure an MQTT broker/service is available; use the Supervisor-provided MQTT service where applicable.
- [ ] Configure only the coordinator-specific serial settings.
- [ ] ZBDongle-P tested baseline: `zstack`, `/dev/ttyUSB0`, `115200` (prefer `/dev/serial/by-id/...` when available).
- [ ] For iHost MG21 via Silicon Labs Multiprotocol: use the add-on hostname TCP endpoint on port `9999` with `ember`, following the iHost add-on documentation.
- [ ] Start Zigbee2MQTT and open its Web UI.
- [ ] Permit Join and pair TYBAC-006.
- [ ] Confirm successful interview and `_TZE204_mpbki2zm`.
- [ ] Install `node-red-contrib-mrsmart-ihost-fcu` in Node-RED.

## Fallback – standalone Docker on CUBE/iHost (validated)

Use this only when the Home Assistant add-on route is not being used.

- [ ] Image: `koenkk/zigbee2mqtt`
- [ ] Network: `bridge`
- [ ] Host port: `8080`
- [ ] Add-on port: `8080`
- [ ] Host volume: `zigbee2mqtt-data`
- [ ] Add-on volume: `/app/data`
- [ ] Environment: `ZIGBEE2MQTT_CONFIG_FRONTEND_ENABLED=true`
- [ ] Select detected Zigbee USB coordinator in iHost Docker Run UI.
- [ ] Map the correct add-on path (tested ZBDongle-P: `/dev/ttyUSB0`).
- [ ] Complete onboarding.
- [ ] Standalone validated MQTT endpoint: `mqtt://172.17.0.1:1884` with base topic `zigbee2mqtt`.
- [ ] Pair thermostat and confirm successful interview.
