---
title: ESP8266 OTA Update Bin
description: 
published: 1
date: 2023-11-10T17:20:29.796Z
tags: 
editor: markdown
dateCreated: 2023-11-09T05:38:15.719Z
---


### Step 1

Download the latest release from [arduino-cli](https://github.com/arduino/arduino-cli)


### Step 2

**Create a file named `.cli-config.yml`** with the below content. I put mine in the same directory as arduino-cli for ease of use.

> By default, arduino searches for this file in `/usr/local/bin/.cli-config.yml`, but I don't recommend you creating such a file in the root partition. You can create it anywhere you want, we just need the path to that file.

```yml
board_manager:
  additional_urls:
    - http://arduino.esp8266.com/stable/package_esp8266com_index.json
```

### Step 3

**Install the core packages for support for the NodeMCU board**.

The package is called `esp8266`. If you install through the arduino IDE boards manager, you will see this name.

> Use the path to the `.cli-config.yml` after `--config-file`, for example, if it's in the current directory (`.`) itself, run this:

```sh
arduino-cli core install esp8266:esp8266 --config-file ./.cli-config.yml
```

> Now if you check the output of `./arduino-cli board listall`. You will find a `NodeMCU 1.0` board.

### Step 4:

Upload to the board:

```sh
./arduino-cli upload -p <esp8266 ip> --input-file <path to bin> --fqbn esp8266:esp8266:generic
```

If it asks for a password and you haven't set one, just press enter to continue

It should output something like:

```
Uploading to specified board using network protocol requires the following info:
Password: 
Uploading..............................................................................................................................................................................................................................................................................................................................................................................
New upload port: 10.0.0.187 (network)
```

