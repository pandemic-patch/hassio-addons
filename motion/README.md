# DCMARTIN Hass.io Add-ons: Motion

Motion add-on by DCMARTIN for Hass.io

## About

This is add-on for the Motion package (https://motion-project.github.io)

It provides for the specification of almost all the configuration options for Motion (https://motion-project.github.io/motion_config.html), 
including the specification of up to 10 (ten) cameras.

## Installation

The installation of this add-on is pretty straightforward and not different in
comparison to installing any other Hass.io add-on.

1. [Add our Hass.io add-ons repository][repository] to your Hass.io instance.
1. Install the "Motion" add-on
1. Configure the "Motion" add-on
1. Start the "Motion" add-on
1. Check the logs of the "Motion" add-on for failures :-(
1. Select the "Open WebUI" button to see the cameras output

**NOTE**: Do not add this repository to Hass.io, please use: `https://github.com/dcmartin/hassio-addons`.

## Docker status

None of this is probably configured properly

[![Docker Architecture][armhf-arch-shield]][armhf-dockerhub]
[![Docker Version][armhf-version-shield]][armhf-microbadger]
[![Docker Layers][armhf-layers-shield]][armhf-microbadger]
[![Docker Pulls][armhf-pulls-shield]][armhf-dockerhub]
[![Anchore Image Overview][armhf-anchore-shield]][armhf-anchore]

[![Docker Architecture][aarch64-arch-shield]][aarch64-dockerhub]
[![Docker Version][aarch64-version-shield]][aarch64-microbadger]
[![Docker Layers][aarch64-layers-shield]][aarch64-microbadger]
[![Docker Pulls][aarch64-pulls-shield]][aarch64-dockerhub]
[![Anchore Image Overview][aarch64-anchore-shield]][aarch64-anchore]

[![Docker Architecture][amd64-arch-shield]][amd64-dockerhub]
[![Docker Version][amd64-version-shield]][amd64-microbadger]
[![Docker Layers][amd64-layers-shield]][amd64-microbadger]
[![Docker Pulls][amd64-pulls-shield]][amd64-dockerhub]
[![Anchore Image Overview][amd64-anchore-shield]][amd64-anchore]

[![Docker Architecture][i386-arch-shield]][i386-dockerhub]
[![Docker Version][i386-version-shield]][i386-microbadger]
[![Docker Layers][i386-layers-shield]][i386-microbadger]
[![Docker Pulls][i386-pulls-shield]][i386-dockerhub]
[![Anchore Image Overview][i386-anchore-shield]][i386-anchore]

## Configuration

The configuration for this add-on includes configuration for the Motion package (https://motion-project.github.io), 
but also for utilization of various services from the IBM Cloud, including Watson Visual Recognition (https://www.ibm.com/watson/services/visual-recognition/).

### Option: `name`

The top-level `name` option controls the identification of the device running the Motion software
Providing a name will consistently identify the configuration utilized during operation.
Defaults to the HOSTNAME environment from Hass.io.  

### Option: `Motion Configuration`

The Motion package has extensive documentation (https://motion-project.github.io/motion_config.html).
The JSON configuration options are provided using the same name as in the Motion documentation.

For example configuration:

```json
{
    "locate_motion_mode":"on",
    "locate_motion_style":"box",
}
```

**Note**: _Remember to SAVE and then restart the add-on when the configuration is changed._

### Option: `cameras`

Some add-on configuration options are for _all_ cameras, as in the example above.

Options which can be specified on a per camera basis are:

1. name (string, non-optional)
1. url (string, non-optional)
1. userpass (string, optional; format "user:pass")
1. keepalive (string, optional; valid {"1.1","1.0","force")
1. port (port, optional; will be calculated)
1. quality \[of captured JPEG image\] (int, optional; valid \[0,100); default 80)
1. width (int, optional; default 640)
1. height (int, optional; default 480)
1. rotate (int, optional; valid (0,360); default 0)
1. threshold \[of pixels changed to detect motion\] (int, optional; valid (0,10000); default 5000)
1. models \[for visual recognition\] (string, optional; format "\[wvr|digits\]:modelname,<model2>,.."bbbbbbb

### Option: `fps`

This option specifies the estimate frames-per-second that are processed to create the event GIF animations

### Option: `mqtt_host` `mqtt_port`

Specify the host and port for sending MQTT messages.  Topics are based on 'motion/{hostname}/{cameraname}' and include sub-topics for '/event/start' and '/event/end'.

### Option: `post_pictures`

This specifies if pictures should be posted to MQTT as they are captured (i.e. "on") _or_ if a single picture should be posted for each event.
The value may be "on" to post every picture; "off" to post no pictures; or one of the following:

1. "best" - the picture with movement closest to the center
1. "center" - the center picture (half-way between start and end of event)
1. "first" - the first picture 
1. "last" - the last picture
1. "most" - the picture with the most pixels changed from previous frame

### Option: `minimum_animate`

The minimum number of images captured during an event that should be animated as a GIF.  Optional.  Default and minimum value is 2.

### Option: `interval`

The maximum time in seconds that will comprise an event; measured backward from the event of the event.  Optional. Default 0; indicating no maximum.

## Changelog & Releases
## Changelog & Releases

This repository keeps a change log using [GitHub's releases][releases]
functionality. The format of the log is based on
[Keep a Changelog][keepchangelog].

Releases are based on [Semantic Versioning][semver], and use the format
of ``MAJOR.MINOR.PATCH``. In a nutshell, the version will be incremented
based on the following:

- ``MAJOR``: Incompatible or major changes.
- ``MINOR``: Backwards-compatible new features and enhancements.
- ``PATCH``: Backwards-compatible bugfixes and package updates.

## Support

Got questions?

You have several options to get them answered:

- The Home Assistant [Community Forum][forum], we have a
  [dedicated topic][forum] on that forum regarding this repository.
- The Home Assistant [Discord Chat Server][discord] for general Home Assistant
  discussions and questions.
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

You could also [open an issue here][issue] GitHub.

## Contributing

This is an active open-source project. We are always open to people who want to
use the code or contribute to it.

We have set up a separate document containing our
[contribution guidelines](CONTRIBUTING.md).

Thank you for being involved! :heart_eyes:

## Authors & contributors

David C Martin (github@dcmartin.com)

The original setup of this repository is by [Franck Nijhof][frenck].

## License

MIT License

Copyright (c) 2017 David C Martin

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[aarch64-anchore-shield]: https://anchore.io/service/badges/image/8f74a497abc908834244d697a67675ecd13080199270598283c8e0cea1b1723e
[aarch64-anchore]: https://anchore.io/image/dockerhub/dcmartin%2Fmotion-aarch64%3Alatest
[aarch64-arch-shield]: https://img.shields.io/badge/architecture-aarch64-blue.svg
[aarch64-dockerhub]: https://hub.docker.com/r/dcmartin/hassioaddons/motion-aarch64
[aarch64-layers-shield]: https://images.microbadger.com/badges/image/dcmartin/hassioaddons/motion-aarch64.svg
[aarch64-microbadger]: https://microbadger.com/images/dcmartin/hassioaddons/motion-aarch64
[aarch64-pulls-shield]: https://img.shields.io/docker/pulls/dcmartin/hassioaddons/motion-aarch64.svg
[aarch64-version-shield]: https://images.microbadger.com/badges/version/dcmartin/hassioaddons/motion-aarch64.svg
[amd64-anchore-shield]: https://anchore.io/service/badges/image/e8858057accd3b85042797097e3ea5b1d80010019bb22a3de32bad5219405319
[amd64-anchore]: https://anchore.io/image/dockerhub/dcmartin/hassioaddons%2Fmotion-amd64%3Alatest
[amd64-arch-shield]: https://img.shields.io/badge/architecture-amd64-blue.svg
[amd64-dockerhub]: https://hub.docker.com/r/dcmartin/hassioaddons/motion-amd64
[amd64-layers-shield]: https://images.microbadger.com/badges/image/dcmartin/hassioaddons/motion-amd64.svg
[amd64-microbadger]: https://microbadger.com/images/dcmartin/hassioaddons/motion-amd64
[amd64-pulls-shield]: https://img.shields.io/docker/pulls/dcmartin/hassioaddons/motion-amd64.svg
[amd64-version-shield]: https://images.microbadger.com/badges/version/dcmartin/hassioaddons/motion-amd64.svg
[armhf-anchore-shield]: https://anchore.io/service/badges/image/a86761f8fb7f0b8e0230dd1c51d01ab2acf97e553fbff0149238853fff9f5d3f
[armhf-anchore]: https://anchore.io/image/dockerhub/dcmartin/hassioaddons%2Fmotion-armhf%3Alatest
[armhf-arch-shield]: https://img.shields.io/badge/architecture-armhf-blue.svg
[armhf-dockerhub]: https://hub.docker.com/r/dcmartin/hassioaddons/motion-armhf
[armhf-layers-shield]: https://images.microbadger.com/badges/image/dcmartin/hassioaddons/motion-armhf.svg
[armhf-microbadger]: https://microbadger.com/images/dcmartin/hassioaddons/motion-armhf
[armhf-pulls-shield]: https://img.shields.io/docker/pulls/dcmartin/hassioaddons/motion-armhf.svg
[armhf-version-shield]: https://images.microbadger.com/badges/version/dcmartin/hassioaddons/motion-armhf.svg
[bountysource-shield]: https://img.shields.io/bountysource/team/hassio-addons/activity.svg
[bountysource]: https://www.bountysource.com/teams/hassio-addons/issues
[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-2.svg
[buymeacoffee]: https://www.buymeacoffee.com/frenck
[commits-shield]: https://img.shields.io/github/commit-activity/y/hassio-addons/motion.svg
[commits]: https://github.com/dcmartin/hassio-addons/motion/commits/master
[contributors]: https://github.com/dcmartin/hassio-addons/motion/graphs/contributors
[discord-shield]: https://img.shields.io/discord/330944238910963714.svg
[discord]: https://discord.gg/c5DvZ4e
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg
[forum]: https://community.home-assistant.io/t/repository-community-hass-io-add-ons/24705?u=frenck
[frenck]: https://github.com/frenck
[dcmartin]: https://github.com/dcmartin
[gitlabci-shield]: https://gitlab.com/hassio-addons/motion/badges/master/pipeline.svg
[gitlabci]: https://gitlab.com/hassio-addons/motion/pipelines
[i386-anchore-shield]: https://anchore.io/service/badges/image/d2cf5186954b12ccd3d31dcc785b36dfc8306ad850b0b29c3ceea4e466b7123a
[i386-anchore]: https://anchore.io/image/dockerhub/dcmartin/hassioaddons%2Fmotion-i386%3Alatest
[i386-arch-shield]: https://img.shields.io/badge/architecture-i386-blue.svg
[i386-dockerhub]: https://hub.docker.com/r/dcmartin/hassioaddons/motion-i386
[i386-layers-shield]: https://images.microbadger.com/badges/image/dcmartin/hassioaddons/motion-i386.svg
[i386-microbadger]: https://microbadger.com/images/dcmartin/hassioaddons/motion-i386
[i386-pulls-shield]: https://img.shields.io/docker/pulls/dcmartin/hassioaddons/motion-i386.svg
[i386-version-shield]: https://images.microbadger.com/badges/version/dcmartin/hassioaddons/motion-i386.svg
[issue]: https://github.com/dcmartin/hassio-addons/motion/issues
[keepchangelog]: http://keepachangelog.com/en/1.0.0/
[license-shield]: https://img.shields.io/github/license/hassio-addons/motion.svg
[maintenance-shield]: https://img.shields.io/maintenance/yes/2018.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[reddit]: https://reddit.com/r/homeassistant
[releases-shield]: https://img.shields.io/github/release/hassio-addons/motion.svg
[releases]: https://github.com/dcmartin/hassio-addons/motion/releases
[repository]: https://github.com/dcmartin/hassio-addons/repository
[semver]: http://semver.org/spec/v2.0.0.html