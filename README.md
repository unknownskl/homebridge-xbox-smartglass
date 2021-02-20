![Homebridge-Smartglass](images/header.png | width=500)

# Homebridge-Smartglass

[![Build and Lint](https://github.com/unknownskl/homebridge-smartglass/actions/workflows/build.yml/badge.svg?branch=release%2F1.0.1)](https://github.com/unknownskl/homebridge-smartglass/actions/workflows/build.yml)
[![npm](https://img.shields.io/npm/v/homebridge-smartglass.svg?style=flat-square)](https://www.npmjs.com/package/homebridge-smartglass)
[![npm](https://img.shields.io/npm/dt/homebridge-smartglass.svg?style=flat-square)](https://www.npmjs.com/package/homebridge-smartglass)


This is a plugin for Homebridge that allows you to control your xbox console. The following features are supported:

- Turn on and off
- Show current active app using input sources
- Allows you to launch apps and games using the input switcher *
- Control volume on the Xbox Series *
- Remote control using the native IOS remote


\* *Requires to be logged in and have the console configured using the Xbox API.*

## Requirements:

- NodeJS >= 10.x
- Homebridge >= 1.1.6

## Installation instructions

Install the plugin:

    npm install -g homebridge-smartglass

## Config UI X / HOOBS instructions

1. Search for the plugin using `smartglass`
2. Install plugin and configure using the UI.

## Setting up the Xbox

The plugin needs to be allowed to connect to your Xbox. To allow this make sure you set the setting to allow anonymous connections in Settings -> Devices -> Connections on the Xbox.

## Homebridge configuration

Configure the Platform in your Homebridge config like below. Replace the ip address and liveid.

    "platforms": [
      {
        "platform": "Smartglass",
        "devices": [
          {
            "name": "Xbox Series S",
            "ipaddress": "192.168.2.9",
            "liveid": "F400000000000000",
            "inputs": [
              {
                "name": "Twitch",
                "aum_id": "TwitchInteractive.TwitchApp_7kd9w9e3c5jra!Twitch",
                "title_id": "442736763"
              },
              {
                "name": "Spotify",
                "aum_id": "SpotifyAB.SpotifyMusic-forXbox_zpdnekdrzrea0!App",
                "title_id": "1693425033"
              },
              {
                "name": "Youtube",
                "aum_id": "GoogleInc.YouTube_yfg5n0ztvskxp!App",
                "title_id": "122001257"
              },
              {
                "name": "Destiny 2",
                "aum_id": "Bungie.Destiny2basegame_8xb1a0vv8ay84!tiger.ReleaseFinal",
                "title_id": "144389848"
              }
            ]
          }
        ]
      }
    ]

| Key | Explanation |
|-----|-------------|
| `name` | The name of the accesory to appear in Homekit |
| `liveid` | This needs to contain your Xbox live id. You can get this live id in the console settings. |
| `ipaddress` | This needs to contain your xbox console ip. Best is to set a static ip on the console. |
| `inputs` | This part is optional. You can define extra apps here to show them in Homekit and you can launch then when you supply a title_id |

### Optional options

The plugin supports optional options for configuring the plugin.

| Key | Explanation |
|-----|-------------|
| `apiToken` | *(Optional)* After authenticating with the Xbox login url you need to paste in the token you get after the redirect in the url (`?code=<code>`) |
| `clientId` | *(Optional)* Provide an Azure AD clientId to use your own tenant for authentication |
| `clientSecret` | *(Optional)* Provide an Azure AD clientSecret related to the clientId to use your own tenant for authentication. Depends on app configuration if needed. |


### Known issues

- TV Controls can stop working after some usage. The client will reconnect when this happens.
