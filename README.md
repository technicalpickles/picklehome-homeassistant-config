# PickleHome HomeAssistant config

Here you'll find the [Home Assistant](https://www.home-assistant.io/) configuration for [PickleHome][picklehome]

## Running

This repository is expected to be cloned to `./homeassistant/config` in a clone of [picklehome][picklehome]. `script/deploy` from the picklehome clone will validate config and restart

## Features

- [house mode, with detection of transitioning from one to another (aka circadian rhythm)](packages/circadian_rhythm.yaml)
- [conference call detected and lights turned on when camera is in use at desk](packages/conference_call.yaml)
- outdoor modes, like [porch mode](packages/porch_mode.yaml) and courtyard mode which turns down the nearby HVAC so it's less noisy
- [fireplace-placed TV with virtual fireplace, and other scenes](packages/fireplace.yaml)
- [christmas cheer](packages/christmas_cheer.yaml)
- [guest mode](packages/guest_mode.yaml) for adjusting thermostat of guest house for when guests are around
- automated forecast-dependent thermostat control, aka [southern comfort](packages/southern_comfort.yaml)
- lighting automation based on [sunrise and sunset](packages/sun.yaml)

## Implementation

The main entry point of this repository is [configuration.yaml](configuration.yaml).

### Patterns

#### Group similar components together

I group config together like:

- packages for functional grouping of automation, templating, etc
- 'core' components homeassistant needs to be used in general (ie frontend, http, history, etc)
- 'automation' components, that don't fit anywhere else
- components for devices and cloud services

#### Use Packages

I make heavy use of [packages][homeassistant-packages] to make functional groups of template & automation components that power a particular feature.

I try not to add components for devices to services in general, preferring to add those to the main `configuration.yaml`.

####  `include!` early and often

I use `!include` a ton here for two reasons:

- it's easy to comment out a component if it seems to be misbehaving
- when developing homeassistant, it's easier to make a simple `configuration.yaml` that just includes the things you are developing
- when developing automations, if you are only working with a few components, you can include

#### It's a secret from everybody

I use [secrets][] so this repository can be open sourced. I keep a template of the `secrets.yaml` as `secrets.yaml.sample`, which can be useful when setting up the first time,and for CI to be able to copy it to secrets.yaml when doing config validation



[picklehome]: https://github.com/technicalpickles/picklehome
[homeassistant-packages]: https://www.home-assistant.io/docs/configuration/packages/
[secrets]: https://www.home-assistant.io/docs/configuration/secrets/
