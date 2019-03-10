# Meros MSS310 Control and Information of API operations

### - Introduction

The Meross MSS310 is an Smart Wi-Fi Plug with Energy Monitor with cloud funcionality to Google Assistant, Amazon Alexa, normally controlled by the Meross APP, so as this module is very cheap, the idea was to connect it with custom APPs and control it from any of the Open Source home monitoring systems frameworks available ( and to learn and get fun in the process ).

### - Hardware Info

At this time there is seem to be two different model version hardware available:

- HW Version 1
   Its powered by Mediatek MT7688KN SoC with an embedded linux OS inside, you can read more details in this page [http://projects.nesrada.de/mss310/index.html](http://projects.nesrada.de/mss310/index.html)
   
- HW Version 2
   It has an Mediatek MT7682SN SoC Arm Cortex-M4 based, probably much more cheap than HW Version 1, the product page is [https://www.mediatek.com/products/smartHome/mt7682](https://www.mediatek.com/products/smartHome/mt7682)

### - Firmware File Details

This files has been taken from the directory **com.meross.meross_1.4.8/assets/** of the android APK
```
mss310-us-v1-rc0115.bin
mss310-us-v2-rc0107.bin
```

- HW Version 1 file structure can be view with binwalk as it seems to be a "standard" package and you can extract individual files with common tools.

```
binwalk com.meross.meross_1.4.8/assets/mss310-us-v1-rc0115.bin

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             uImage header, header size: 64 bytes, header CRC: 0x524CEFFA, created: 2018-08-09 01:31:13, image size: 742084 bytes, Data Address: 0x80500000, Entry Point: 0x80500000, data CRC: 0xF6CD2850, OS: Linux, CPU: MIPS, image type: Standalone Program, compression type: none, image name: "zxrouter"
9344          0x2480          LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 2179028 bytes
```

- HW Version 2 file structure cannot be extracted as is seems to be an Over The Air Flash package, probably made with Mediatek FOTA ROM Package tool [https://docs.labs.mediatek.com/resource/mt7687-mt7697/en/downloads](https://docs.labs.mediatek.com/resource/mt7687-mt7697/en/downloads)

It seems posible to decode the FOTA file and get the real binaries if you can get access to the required tools, many of the SDK from Mediatek are license bases and they are not public available.

The process of Firmware Update are initiated by an JSON request to the module

### - URL Of Interests

* Photos, serial connection, and information in how to setup the module to connect to an custom MQTT Server

   [https://github.com/bytespider/Meross](https://github.com/bytespider/Meross)
   
* Python script to connect Meross Cloud API and gather useful information

   [https://github.com/bapirex/meross-api](https://github.com/bapirex/meross-api)

* Python API to connect Meross Cloud service and control modules

   [https://github.com/albertogeniola/MerossIot](https://github.com/albertogeniola/MerossIot)
