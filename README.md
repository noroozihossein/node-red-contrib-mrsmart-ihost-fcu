# node-red-contrib-mrsmart-ihost-fcu

Mr Smart FCU integration for SONOFF iHost / Node-RED, designed for the Tuya TYBAC-006 fan-coil thermostat (`_TZE204_mpbki2zm`) through Zigbee2MQTT.

## Features

- Native Node-RED node for iHost
- Zigbee2MQTT device auto-discovery
- FCU temperature, setpoint, operating mode and fan-speed control
- Bidirectional state synchronization
- eWeLink CUBE Web custom UI registration
- CUBE CAST custom UI registration
- Installer-supplied iHost address and MQTT port; no site-specific IP or MQTT port is pre-filled

## Installation

Install the package from Node-RED **Manage palette**, or install the packaged `.tgz` file for local testing.

The installer must configure the iHost connection and the MQTT broker port used by the iHost Mosquitto container. The MQTT host can be left blank to use the configured iHost address.

## Supported thermostat

Initial validated target: TYBAC-006 / Tuya TS0601, manufacturer fingerprint `_TZE204_mpbki2zm`.

## License

MIT
