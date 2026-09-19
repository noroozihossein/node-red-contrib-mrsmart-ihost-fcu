# node-red-contrib-mrsmart-ihost-fcu

Mr Smart FCU integration for SONOFF iHost / Node-RED, designed for the Tuya TYBAC-006 fan-coil thermostat (`_TZE204_mpbki2zm`) through Zigbee2MQTT.

## Features

- Native Node-RED node for iHost
- Zigbee2MQTT device auto-discovery
- Installer device picker populated from `zigbee2mqtt/bridge/devices`
- Multi-thermostat support: use one FCU node per thermostat and select each device independently
- Stable IEEE-address binding with automatic Friendly Name/topic resolution after a rename
- FCU temperature, setpoint, operating mode and fan-speed control
- Bidirectional state synchronization
- eWeLink CUBE Web custom UI registration
- CUBE CAST custom UI registration
- Installer-supplied iHost address and MQTT port; no site-specific IP or MQTT port is pre-filled

## Installation

Install the package from Node-RED **Manage palette**, or install the packaged `.tgz` file for local testing.

The installer must configure the iHost connection and the MQTT broker port used by the iHost Mosquitto container. The MQTT host can be left blank to use the configured iHost address.

Select **Refresh Devices** in the FCU node editor, then choose the required thermostat from the dropdown. Zigbee2MQTT creates a Friendly Name automatically when a device joins; renaming it is optional. The node stores the device IEEE address as its stable identity and resolves the current Friendly Name for MQTT topics.

For multiple fan-coil zones, add one FCU node per thermostat. New nodes use their Node-RED node ID as the UI instance identifier when Instance ID is left blank, preventing Web/CAST route collisions. Existing flows with a manually configured Instance ID remain compatible.

## Supported thermostat

Initial validated target: TYBAC-006 / Tuya TS0601, manufacturer fingerprint `_TZE204_mpbki2zm`.

## License

MIT
