# Xiao-ESP32S3-Sense-Enhanced
This project's goal is to make the Xiao ESP32S3 Sense a viable option as a surveillance camera accessible from the Internet.

## Warning
This code only works for SeeedStudio's Xiao ESP32S3 Sense, with OPI PSRAM enabled, and any of the supported cameras (OVs 2640, 3660 and 5640).
Webpage/camera speed is not guaranteed due to the heavy resource usage of the code.

> Enable OPI PSRAM in Arduino IDE: Open your board sketch > `Tools` > `PSRAM` > `OPI PSRAM`

## Current Changes

# The changes listed below are only a fraction of the new implemented features. Check each update to see what it adds.

### Operating on a Single Port
Most routers block or do not give you access to port 81, which is the one the board uses for streaming. With the original code, it would be impossible to see the stream outside a local network.
The hardcoded lines have been disabled, and the stream was merged to port 80, which the board already uses to manage the webpage.

### Flexible Byte Array Indexes
Made the board read the lenght of the webpage array instead of hardcoded values. These values are kept in but are not used anymore.
Changes were made to the webpage as well to make it stop using the hardcoded address (address + :81) and made it use the new flexible route instead (address + /stream).
Since the board hands out a different webpage for every camera model, this change had to be done to all three compressed byte arrays which compose the webpage (OV2640, OV3660 and OV5640).

### HTTPS Integration
The web server now runs on HTTPS (self-signed certificates are allowed), for encryption. When using self-signed certificates, browsers will show a security risk page by default.
> This change sacrifices overrall speed for security.
> Certificates must be put in `certs.h` and need to be formatted correctly. 

### Simple Authentication
The webpage asks for the correct username and password before loading anything.

## Configuration

### `config.h`
Allows you to change SSID, WiFi password, Internal Port, Username and Password for the camera

### `certs.h`
Input your certificate and private key here to allow HTTPS to work.

> No need to touch other code.
