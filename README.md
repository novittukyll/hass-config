# My Home Assistant configuration

![Screenshot](/assets/images/screenshot.png)

## Introduction

My home assistant journey started roughly 2018 but was not very active for the first two years. I was happy with the default lovelace UI for a while until I started to notice projects that took completely different approach on designing their dashboards.

Significant inspiration started when I came across [UI-Lovelace-Minimalist](https://github.com/UI-Lovelace-Minimalist/UI) project and further studied [@matt8707](https://github.com/matt8707/hass-config)'s great design!

After learning how to use the brilliant and very flexible [button-card](https://github.com/custom-cards/button-card) by [@RomRider](https://github.com/RomRider) I came up with my current design for tablet and mobile. Yes, this design is heavily based on the button-card. Maybe I went a bit too deep with it...

Hope you enjoy and find things useful in this repo! ⭐

## Setup

Home Assistant runs on [Docker](https://hub.docker.com/r/homeassistant/home-assistant) on a [Synology NAS](https://www.synology.com). Users access Home Assistant through the [Companion App](https://companion.home-assistant.io) on their mobile. In addition, the house has table mounted [10.5" Samsung Galaxy Tab A8](https://www.samsung.com/uk/tablets/galaxy-tab-a/galaxy-tab-a8-wifi-dark-gray-32gb-sm-x200nzaaeua/).

Configuration is performed mostly using YAML.

The following custom cards are extensively used throughout the dashboards:

- [button-card](https://github.com/custom-cards/button-card)
- [mini-graph-card](https://github.com/kalkih/mini-graph-card)
- [card-mod](https://github.com/thomasloven/lovelace-card-mod)
- [layout-card](https://github.com/thomasloven/lovelace-layout-card)
- [light-entity-card](https://github.com/ljmerza/light-entity-card)
- [weather-chart-card](https://github.com/Yevgenium/weather-chart-card)
- [apexcharts-card](https://github.com/RomRider/apexcharts-card)
- [xiaomi-vacuum-map-card](https://github.com/PiotrMachowski/lovelace-xiaomi-vacuum-map-card)

## Features

### Sidebar, notifications and clock

- Fancy sidebar clock with date, time, current weather condition and outdoor temperature
- Conditional notifications such as doors open, precipitation, Home Assistant and Synology updates etc.
- Notification badge in the home card (useful especially on mobile)

Few notifications that can be visible on the sidebar

- Heat pump alarm
- Doors open
- High CO2
- High and low indoor humidity
- High radon levels
- Garage dehumidifier on
- Current and today's precipitation
- Vacation mode on
- Synology security state warning
- Synology update available
- Home Assistant update available
- Vacuuming state
- Time to vacuum
- Vacuum dustbin is full

### Custom button cards

I have created few [button card templates](button_card_templates/troinine) for my own needs. To mention few:

- Generic info card with extra entity
- Generic sensor card
- Graph sensor card (graph displayed with mini-graph-card)
- Sidebar clock with date, time and weather
- Light card with a slider
- User card with device tracker and battery statuses
- Notification card that is used in the sidebar
- Vacuum card with buttons to control the robot vacuum
- Media card with buttons to control the media player
- Conditional card which allows flexible way of conditionally showing or hiding a card

All cards try to incorporate similar design. Icons can glow based on the state and the light card has a glowing box shadow when the respective light is on.

#### Clock

Clock is a button card template that show the current date, time, temperature, and weather

![Clock](/assets/images/screenshot-clock.png)

The tap action on the weather shows the following popup which uses [weather-chart-card](https://github.com/Yevgenium/weather-chart-card) and an apexchart of outdoor temperature:

![Weather](/assets/images/screenshot-weather.png)

### Popups

Popups have been implemented using [browser_mod](https://github.com/thomasloven/hass-browser_mod). Here are few examples:

Custom light popup with predefined scenes and color wheel. This card has few features:

- Can support `light.` and `switch.` entities and select features based on that
- Allows explicitly enabling or disabling the color wheel
- Allows explicitly enabling or disabling presets for specific colors

![Light popup](/assets/images/screenshot-light-popup.png)

Air quality popup. Each room is a separate [swipe-card](https://github.com/bramkragten/swipe-card) page:

![Air quality popup](/assets/images/screenshot-air-quality-popup.png)

Heating data popup:

![Heating popup](/assets/images/screenshot-heating-popup.png)

Mobile notifications popup:

![Mobile notifications popup](/assets/images/screenshot-mobile-notifications-popup.png)

Mobile popup with cards:

![Mobile popup](/assets/images/screenshot-mobile-popup.png)

### Automations

In addition to basic lights on / off based on movement. There are few automations that I use

- Wake up tablet and increase light brightness when movement is detected in the hallway
- Notify mobile app if the garage dehumidifier's bucket is full
- Turn hallway lights on when garage door is opened (arrive home)
- Start vacuuming when leaving home if it hasn't been done for few days
- Notify mobile app if the ground source heat pump reports an alarm
- Notify mobile app when Radon levels are increasing
- Notify mobile app when vacuum is started and completed

## Hardware and software

The following table contains some of the hardware and software I use with Home Assistant

| Product                     | Integration        | Description                                                                                                                                                                                         |
| --------------------------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Airthings Wave Plus         | MQTT               | Two Airthings Wave Plus sensors measuring temperature, humidity, CO2, VOC and Radon                                                                                                                 |
| Philips Hue                 | Philips Hue        | Philips Hue Bridge with light strips, bulbs, motion sensors, dimmer switches                                                                                                                        |
| Synology DiskStation DS220+ | Synology DSM       | NAS which runs Home Assistant and bunch of other services for my needs                                                                                                                              |
| Ruuvi                       | MQTT               | A bunch of RuuviTags. I have a custom-built software that reads data from these tags                                                                                                                |
| Raspberry Pi Zero           | MQTT               | Provides near real-time data from the ground source heat pump. Reads data from RuuviTags. Is equipped with [Readbear's IOT pHAT](https://github.com/redbear/IoT_pHAT) for Wifi and BT connectivity. |
| Nibe 1226 NEW 8kW           | MQTT               | Ground source heat pump providing heating and cooling to the house                                                                                                                                  |
| Sony Playstation 5          | CLI                | Only PS5 status is currently retrieved via CLI                                                                                                                                                      |
| Samsung TV                  | Samsung Smart TV   | Samsung Q90 Series Smart TV                                                                                                                                                                         |
| Nokia Streaming Box 8000    | Android TV         | Nokia Streaming Box to make one of my dummy TV's smart                                                                                                                                              |
| Yale Doorman                | Verisure           | Smart locks securing the house doors                                                                                                                                                                |
| TP-Link Kasa Smart plugs    | TP-Link Kasa Smart | Few HS100 and HS110 smart plugs controlling specific devices such as garage dehumidifier and water circulation                                                                                      |
| Roborock S6 Pure            | Xiaomi Mi          | Robot vacuum which can be controlled via HA, including cleaning of specific rooms. Live map is also available                                                                                       |

In addition to hardware I use a collection of OSS to feed data to Home Assistant:

| Software                                                                                                     | Description                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ruuvi-mqtt-data-publisher](https://github.com/troinine/ruuvi-mqtt-data-publisher)                           | A forked version of [Scrin/RuuviCollector](https://github.com/Scrin/RuuviCollector) that reads data from RuuviTags and publishes it to an MQTT Broker |
| [airthings-waveplus-mqtt-data-publisher](https://github.com/troinine/airthings-waveplus-mqtt-data-publisher) | Reads data from Airthings Wave Plus sensors and publishes it to an MQTT broker                                                                        |
| [Eclipse Mosquitto](https://mosquitto.org)                                                                   | Receives data from various MQTT clients and is observed by Home Assistant                                                                             |
| Nibe heat pump MQTT data publisher                                                                           | Custom-built app that reads Nibe heat pump logs through an USB OTG mass-storage emulation and publishes the data to an MQTT broker                    |
| [Scrapy](https://scrapy.org)                                                                                 | Custom web site scraper that obtains electricity consumption from [Helen](https://www.helen.fi) and sends the data to an MQTT broker                  |

## License

This repo is [MIT Licensed](LICENSE)
