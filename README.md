# Xiao-ESP32S3-Sense-Enchanced
Making changes to the Xiao ESP32S3 Sense Dev Board with the goal of making it easier to use.

# Warning
This code only works for SeeedStudio's Xiao ESP32S3 Sense, with OPI PSRAM enabled, and any of the supported cameras (OVs 2640, 3660 and 5640)

---------------------------

## Current Changes

### Operating on a Single-Port
Most routers block or do not give you access to port 81, which is the one the board uses for streaming. With the original code, it would be impossible to see the stream outside a local network.
The hardcoded lines have been disabled, and the stream was merged to port 80, which the board already uses to manage the webpage.

Changes were made to the webpage as well to make it stop using the hardcoded address (address + :81) and made it use the new flexible route instead (address + /stream).
Since the board hands out a different webpage for every camera model, this change had to be done to all three compressed byte arrays which compose the webpage (OV2640, OV3660 and OV5640).

### Flexible Byte Array Indexes
Made the board read the lenght of the array instead of hardcoded values. These values are kept in but are not used anymore.
