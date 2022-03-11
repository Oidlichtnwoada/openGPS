# openGPS Setup

## Used Hardware

1. two **simpleRTK2B** basic starter kits
   available [here](https://www.ardusimple.com/product/simplertk2b-basic-starter-kit-ip65/)
2. two USB cables available [here](https://www.amazon.de/AmazonBasics-Male-Micro-Cable-Black/dp/B07232M876/)
3. one **Raspberry Pi** available [here](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
4. one charger for the **Raspberry Pi** available [here](https://www.raspberrypi.org/products/type-c-power-supply/)
5. one microSD card with adapter for the **Raspberry Pi**
   available [here](https://www.amazon.de/SanDisk-Ultra-Micro-Adapter-SDSQUNC-016G-GN6MA/dp/B010Q57SEE/)
6. one computer that meets the requirements
   presented [here](https://geizhals.at/?cat=nb&xf=10929_Windows+10%7E13345_LTE%7E13732_2%7E2379_15%7E83_Touchscreen%7E9_1920x1080)
7. one Wi-Fi router with internet access near the **Raspberry Pi**
8. one voltage transformer to operate the computer with 12V
   available [here](https://www.amazon.de/Spannungswandler-Wechselrichter-BESTEK-Zigarettenanzünder-Autobatterieclips/dp/B00JGJL4ZQ/)

## simpleRTK2B Setup

1. download the latest **u-center** software [here](https://www.u-blox.com/en/product/u-center)
2. download the latest firmware
   update [here](https://www.u-blox.com/en/product/zed-f9p-module#tab-documentation-resources)
3. install the firmware update on both **simpleRTK2B** boards using the tutorial
   provided [here](https://www.ardusimple.com/zed-f9p-firmware-update-with-simplertk2b/)
4. apply the **Base**, and the **Rover 10Hz** configuration to each of the **simpleRTK2B** boards
   provided [here](https://cerea-forum.de/filebase/index.php?file/18-ublox-f9p-config-file/)
5. the **Base** configuration must be adjusted by setting the position of the **Base** station in the Configuration
   View (Ctrl+F9) under the point TMODE3 and saving it afterwards, a tutorial is
   provided [here](https://www.youtube.com/watch?v=FpkUXmM7mrc)

## RTK2go Setup

1. configure a mountpoint and a password for it on the RTK2go NTRIP
   server [here](http://www.rtk2go.com/new-reservation/), follow the instructions on the website and leave all settings
   to the default where possible

## Raspberry Pi Setup

1. download the latest **Raspberry Pi OS** Lite image [here](https://www.raspberrypi.org/software/operating-systems/)
2. download the latest **balenaEtcher** software [here](https://www.balena.io/etcher/)
3. flash the **Raspberry Pi OS** Lite image to the **Raspberry Pi** microSD Card using **balenaEtcher**
4. create a file named ssh without any content in the root of the boot partition
5. create a file named wpa_supplicant.conf in the same directory with the required information filled in, a template is
   provided [here](https://medium.com/coinmonks/run-raspberry-pi-in-a-true-headless-state-cfb3431667de)
6. the previous link also provides a description how to connect to the **Raspberry Pi** via SSH, follow it and connect
   to the device
7. execute the commands ```sudo apt update``` and ```sudo apt full-upgrade``` to install the latest packages on your
   **Raspberry Pi**
8. execute the command ```sudo apt install rtklib``` to execute the required library on your **Raspberry Pi**
9. fill in the password (PASSWD) and the mountpoint (MNTPNT) of the RTK2go NTRIP server in
   this [service file](base.service)
10. use ```scp``` to copy the filled service file to the **Raspberry Pi** home directory as
    described [here](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/)
11. copy the service file from the home directory to the folder ```/etc/systemd/system/``` using the ```cp``` command
12. execute the command ```sudo systemctl enable base.service``` to start this service at the next boot up
13. reboot the **Raspberry Pi** using the command ```sudo reboot```, you will have to reconnect to SSH again after the
    device has rebooted
14. after reconnecting check that the command ```sudo systemctl status base.service``` returns the status active








