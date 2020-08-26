# `cpu2msghub` -  addon for Home Assistant

This [Home Assistant][home-assistant] add-on is for the [Open Horizon][open-horizon] [`cpu2msghub`][cpu-pattern] pattern.

This add-on requires the [setup][dcm-oh] of Horizon, a distibuted, decentralized, zero-ops, method and apparatus to deploy containers from the IBM Cloud.

**Note**: _You will need an IBM Cloud [account][ibm-registration]_

**Note**: _You must obtain a Kafka API key; request one in the IBM Edge Fabric [Slack][edge-slack]_

## About

This addon is designed to produce and consume messages containing CPU usage and GPS coordinates (latitude, longitude) from  participating nodes on a _private_ Kafka topic using IBM Message Hub in the IBM Cloud.  Kafka CPU messages from the `cpu2msghub` pattern are captured and processed by this addon to produce a JSON payload sent to a MQTT broker, e.g. [`core-mosquitto`][core-mosquitto] from the HASSIO addons catalog.

Detailed [documentation][edge-fabric] for the IBM Edge Fabric is available on-line.  A Slack [channel][edge-slack] is also available.

## Installation

### Install Open Horizon (OPTIONAL)

Please refer to the [`open-horizon`][dcm-oh] repository.

### Install addon

1. [Add this repository][repository] to your Hass.io addon store
1. Install the "cpu2msghub" add-on
1. Setup the "cpu2msghub" add-on
  - Configure `kafka` with your IBM MessageHub API key
  - Configure `horizon` with your IBM Cloud username and [Platform API key][ibm-apikeys]
  - Optionally change `mqtt` for `host`, `port`, `topic`, `username`, and `password`
1. Start the "cpu2msghub" add-on
1. Check the logs of the add-on for failures :-(

## Configuration

### Option: `listen`

Listen mode; (`true`|`false`|`only`); `false` will not listen; *default* is `only` and does not register pattern.

### Option: `horizon`
Credentials required for interacting with the Open Horizon exchange. These options are ignored if Open Horizon is not installed or if `listen` option is set to `only`.  Options for `device` and `token` may be specified, but will *default* to the hostname  (e.g. `cb7b3237_cpu2msghub-192168140`) and the exchange password.  Changing the `device` identifier will force unregistration and re-registration of the pattern.
```
  "horizon": {
    "password": "<Your IBM Cloud Platform API key>",
    "organization": "<Your IBM Cloud login email address>",
    "username": "iamapikey",
    "exchange": "https://alpha.edge-fabric.com/v1"
  }
```

### Option: `kafka`
Credentials required for sending and receiving messages using the IBM Cloud MessageHub.
```
  "kafka": {
    "api_key": "<Your IBM Edge Fabric MessageHub API key>",
    "brokers": "kafka03-prod02.messagehub.services.us-south.bluemix.net:9093,kafka04-prod02.messagehub.services.us-south.bluemix.net:9093,kafka01-prod02.messagehub.services.us-south.bluemix.net:9093,kafka02-prod02.messagehub.services.us-south.bluemix.net:9093,kafka05-prod02.messagehub.services.us-south.bluemix.net:9093"
  }
```

### Option: `mqtt`
This option provides the information required for MQTT service; defaults are as specified below.
```
  "mqtt": {
    "host": "core-mosquitto",
    "port": 1883,
    "topic": "kafka/cpu-load"
    "username": "",
    "password": ""
  }
```

## USE

Listen to the MQTT host and port to receive JSON payload of the processed CPU load.

1. `kafka/cpu-load`

Configuration examples are provided for processing the JSON:

1. Edit your HomeAssistant configuration YAML to include [cpu2msghub][cpu-yaml]
1. Edit your `ui-lovelace.yaml` configuration for [display][cpu-lovelace]

# Sample output

![cpu2msghub cpu](cpu2msghub_cpu.png?raw=true "CPU2MSGHUB")

## Changelog & Releases

Releases are based on Semantic Versioning, and use the format
of ``MAJOR.MINOR.PATCH``. In a nutshell, the version will be incremented
based on the following:

- ``MAJOR``: Incompatible or major changes.
- ``MINOR``: Backwards-compatible new features and enhancements.
- ``PATCH``: Backwards-compatible bugfixes and package updates.

## Authors & contributors

David C Martin (github@dcmartin.com)

[cpu-lovelace]: https://raw.githubusercontent.com/dcmartin/hassio-addons/master/cpu2msghub/ui-lovelace.yaml
[cpu-yaml]: https://raw.githubusercontent.com/dcmartin/hassio-addons/master/cpu2msghub/cpu2msghub.yaml

[commits]: https://github.com/dcmartin/hassio-addons/cpu2msghub/commits/master
[contributors]: https://github.com/dcmartin/hassio-addons/cpu2msghub/graphs/contributors
[issue]: https://github.com/dcmartin/hassio-addons/cpu2msghub/issues
[releases]: https://github.com/dcmartin/hassio-addons/cpu2msghub/releases

[dcmartin]: https://github.com/dcmartin
[repository]: https://github.com/dcmartin/hassio-addons
[dcm-oh]: https://github.com/dcmartin/open-horizon
[dcm-oh-setup]: https://github.com/dcmartin/open-horizon/tree/master/setup
[cpu-pattern]: https://github.com/open-horizon/examples/tree/master/edge/msghub/cpu2msghub
[sdr-pattern]: https://github.com/open-horizon/examples/tree/master/edge/msghub/sdr2msghub
[cpu-addon]: https://github.com/dcmartin/hassio-addons/tree/master/cpu2msghub
[sdr-addon]: https://github.com/dcmartin/hassio-addons/tree/master/sdr2msghub
[horizon-addon]: https://github.com/dcmartin/hassio-addons/tree/master/horizon

[core-mosquitto]: https://github.com/hassio-addons/repository/tree/master/mqtt
[edge-fabric]: https://console.test.cloud.ibm.com/docs/services/edge-fabric/getting-started.html
[edge-install]: https://console.test.cloud.ibm.com/docs/services/edge-fabric/adding-devices.html
[edge-slack]: https://ibm-appsci.slack.com/messages/edge-fabric-users/
[home-assistant]: https://home-assistant.io/
[hzn-setup]: https://raw.githubusercontent.com/dcmartin/hassio-addons/master/horizon/hzn-setup.sh
[ibm-apikeys]: https://console.bluemix.net/iam/#/apikeys
[ibm-registration]: https://console.bluemix.net/registration/
[keepchangelog]: http://keepachangelog.com/en/1.0.0/
[macos-install]: https://github.com/open-horizon/anax/releases
[open-horizon]: https://github.com/open-horizon
[watson-nlu]: https://console.bluemix.net/catalog/services/natural-language-understanding
[watson-stt]: https://console.bluemix.net/catalog/services/speech-to-text
