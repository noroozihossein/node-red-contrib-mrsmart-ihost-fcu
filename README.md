# Mr Smart – iHost Zigbee2MQTT Setup

Recommended installer path for using Zigbee2MQTT on SONOFF iHost as a prerequisite for the Mr Smart iHost FCU Node-RED integration.

## Recommended path: iHost Home Assistant add-on

The iHost Open Source Project provides an iHost-specific Home Assistant add-on repository which includes `hassio-ihost-zigbee2mqtt`. This is the preferred installation path when Home Assistant OS is running on iHost because it avoids manually creating the Zigbee2MQTT Docker container, port mapping and persistent volume.

Add this repository in Home Assistant:

`Settings -> Add-ons / App Store -> ⋮ -> Repositories`

Repository:

`https://github.com/iHost-Open-Source-Project/hassio-ihost-addon`

Then install **iHost Zigbee2MQTT**.

## What is automated

With the add-on path, the add-on handles the Zigbee2MQTT application/container lifecycle and frontend. If a Home Assistant MQTT service is available, the Zigbee2MQTT add-on can obtain the MQTT server and credentials from that service instead of requiring them to be typed into Zigbee2MQTT manually.

The installer still has to select/configure the Zigbee coordinator because this is hardware-specific.

## Coordinator options

### External SONOFF ZBDongle-P / CC2652P (tested)

Use the serial device exposed to Home Assistant/iHost. Typical tested settings are:

```yaml
serial:
  port: /dev/ttyUSB0
  adapter: zstack
  baudrate: 115200
```

Prefer the persistent `/dev/serial/by-id/...` path when the system exposes one.

### iHost internal MG21 / supported Silicon Labs radio

The iHost Open Source Project also provides **Silicon Labs Multiprotocol**. When that add-on is used for Zigbee, Zigbee2MQTT connects to its TCP endpoint using `ember`, for example:

```yaml
serial:
  adapter: ember
  port: tcp://<MULTIPROTOCOL-ADDON-HOSTNAME>:9999
  baudrate: 115200
```

Follow the iHost Multiprotocol add-on documentation for the exact hostname/device and firmware requirements.

## MQTT

Preferred: use the MQTT broker/service already available in the Home Assistant environment so the Zigbee2MQTT add-on can consume the Supervisor MQTT service automatically.

If an external/custom broker is used, enter its server and credentials in the Zigbee2MQTT add-on configuration instead.

For the standalone Docker method previously validated on CUBE/iHost, the tested broker endpoint was `mqtt://172.17.0.1:1884`. That value is **not** a universal Home Assistant add-on value and should not be copied into an add-on installation unless it matches that installation.

## Pair TYBAC-006

1. Start Zigbee2MQTT and open its Web UI.
2. Enable Permit Join.
3. Put the thermostat into Zigbee pairing mode.
4. Wait for a successful interview.
5. Confirm `TYBAC-006 / TS0601` and manufacturer `_TZE204_mpbki2zm`.
6. If the first interview fails after the device joins, re-pair it before reinstalling Zigbee2MQTT; this occurred once during ZBDongle-P validation and the next interview completed successfully.

## Install Mr Smart FCU

After Zigbee2MQTT is operational and TYBAC-006 is paired:

1. Open Node-RED -> Manage Palette -> Install.
2. Install `node-red-contrib-mrsmart-ihost-fcu`.
3. Configure the iHost connection/token.
4. Configure/select the MQTT connection used by Zigbee2MQTT.
5. Select/discover the TYBAC-006.
6. Deploy and verify CUBE Web and CAST.

## Fallback: standalone Docker on CUBE/iHost

If Home Assistant OS/add-ons are not being used, the standalone `koenkk/zigbee2mqtt` Docker method remains valid. See `IHOST-RUN-CHECKLIST.md` for the tested CUBE/iHost Docker settings.

## Why there is no custom one-click Mr Smart installer

iHost/HA add-ons already provide the supported application lifecycle. The remaining non-universal step is coordinator selection/configuration: different radios use different device paths and adapter drivers. A Node-RED package should not attempt to take over host USB passthrough or guess the coordinator. Using the iHost add-on therefore removes the repeatable manual Docker work while leaving only the hardware-specific choice with the installer.
