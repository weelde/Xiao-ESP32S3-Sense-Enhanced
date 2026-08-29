# Xiao-ESP32S3-Sense-Enhanced

Better streaming, better security, better ease of use; all on a tiny finger-sized board.

----------------------------------------------------------------------------------------------------

## Disclaimer

- This project is specifically built for the XIAO ESP32S3 Sense, other boards are untested! Proceed at your own risk.
- This project uses Arduino IDE'S CameraWebServer as a base, with tweaked code and added sections to enhance the experience. All rights to the respective owners.

----------------------------------------------------------------------------------------------------

## Prerequisites

- A PC or Laptop with Arduino IDE installed
- Xiao ESP32S3 Sense board (duh)
- An Internet connection (duhhh)

----------------------------------------------------------------------------------------------------

## Features

- HTTPS
- Basic authentication
- Remote restart/shutdown functions
- Storing logs
- Storing pictures
- A config to tweak all the desired settings
- Differently colored webpages depending on what camera model is used
- Access from outside the local network (see Network section)

----------------------------------------------------------------------------------------------------

## Instructions

### Project
- Download the latest release, extract it and open it in Arduino IDE
- Go to "Boards Manager", search for "esp32" and install the latest "esp32 boards" by Espressif
- Go to "Tools", "Board", "esp32", and select "XIAO_ESP32S3"
- Go to "Tools", "PSRAM", and select "OPI PSRAM"

----------------------------------------------------------------------------------------------------

## Network

> **All routers are different, therefore a precise procedure cannot be given to this step.**

### IP Reservation
Most (if not all) routers reassign random private IPs after some time has elapsed. If a static IP is not set, the camera might fail at any moment during the IP reassigning phase.

- Connect to WiFi and log into your router
- Find a setting like "IP Reservation", "Static IP" or similiar (you might have to enable some kind of "Expert User" mode in order to access this settings)
- Once located, connect the camera to the computer using a USB-C to USB-A type cable and assign an IP of choice to the camera like so
<img width="690" height="280" alt="image" src="https://github.com/user-attachments/assets/b00cb246-3a09-4fe4-b6ed-5a977202d7b8" />
- Save changes if necessary

The camera will get the same IP each time the router will reassign them

--------------------

### Port Forwarding
We're going to redirect certain external traffic to the camera so we can see the live feed from outside the newtwork.

- Connect to WiFi and log into your router
- Find a setting like "Port Forwarding", "Port Mapping", "Virtual Server" or similiar (you might have to enable some kind of "Expert User" mode in order to access this settings)
- Once located, make the following changes (make a new rule if necessary):
> **(Note that 192.168.1.6 is the new, static IP of the camera; Be sure to input that)**:
> **(Also be sure to open ports numbered 443 specifically)**:
<img width="695" height="231" alt="image" src="https://github.com/user-attachments/assets/fc537c7b-40e0-4bbb-af6c-3a2780869c2e" />
- Save changes if necessary

--------------------

### Custom DDNS
This is the last networking step, I swear.

- While connected to WiFi, find your Public IP ([whatismyip](https://whatismyipaddress.com/)
- Sign up on any DDNS service (preferably [[noip]https://no-ip.com](https://www.noip.com/)) (don't worry, you can make one domain for free)
- Register a domain with type-A and with your public IP like so:
<img width="741" height="76" alt="image" src="https://github.com/user-attachments/assets/1da78e38-f1fd-47c5-af7d-5e8dff4a5d6b" />
- Save/Register the new domain

- Log into your router
- Find a setting like "DDNS" or similiar (you might have to enable some kind of "Expert User" mode in order to access this settings)
- Make the following changes:
<img width="728" height="426" alt="image" src="https://github.com/user-attachments/assets/8218a624-7f42-4578-b32b-f7e23b425d2f" />
- Save changes if necessary

--------------------

### Config
Configure the camera (MUST-DO!!)

- Open `config.h` inside the `settings` folder using a text editor and follow the commented instructions

--------------------

### Certificates
Configure the certificates (MUST-DO!!)

- Generate SSL certificates for HTTPS to work (Self-signed certificates work fine, but browsers will display a warning text; That's normal and you can proceed regardless) (You may use OpenSSL or any other tool)
- Paste the contents of the the key and the certificate like so in `settings` -> `certs.h`:
> **(Remember to go to a new line (\n) each line)**
> **(DO NOT share these with anybody)**
> <img width="589" height="862" alt="image" src="https://github.com/user-attachments/assets/3863ab70-6089-46e3-ae79-38c4c92bdd25" />

--------------------

### Uploading

- Connect the board to the computer if it wasn't connected already
- In Arduino IDE, upload the code (top left, Arrow Button)
- Wait for it to finish
- Once it's done, go in any browser and type yourdomaniname.ddns.net
- Input the credentials you chose
- Enjoy the video stream!
> Browsers automatically save credentials so you might not be prompted to log in each time you visit the page
