---
title: ESP8266 OTA Update Bin
description: 
published: 1
date: 2023-11-09T05:38:15.719Z
tags: 
editor: markdown
dateCreated: 2023-11-09T05:38:15.719Z
---


### Step 1

Download [arduino-cli](https://github.com/arduino/arduino-cli)


### Step 2

**Create a file named `.cli-config.yml`** with the below content.

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

> Now if you check the output of `arduino-cli board listall`. You will find a `NodeMCU 1.0` board.

### Step 4:

Then upload to the board:

```sh
./arduino-cli upload -p <arduino ip> --input-file <path to bin> --fqbn esp8266:esp8266:generic
```

It should output something like:

```
esptool.py v3.0
Serial port /dev/ttyUSB0
Connecting....
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: 4c:75:25:37:40:e5
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 289216 bytes to 210989...
Wrote 289216 bytes (210989 compressed) at 0x00000000 in 18.6 seconds (effective 124.3 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```

