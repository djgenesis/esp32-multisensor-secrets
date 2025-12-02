The purpose is the same with [esp32-multisensor](https://github.com/djgenesis/esp32-multisensor) but with secrets file added to the process).

Steps to follow to flash multiple ESP32 with the same .bin file and be auto discovered and adopted by ESPHome - and then Home Assistant - as unique devices.
The devices can be discovered and adopted straight into Home Assistant without being adopted necessarily in ESPHome.
The purpose of having them in ESPHome as well though is to be able to Update them once in a while whenever new ESPHome/Home Assistant changes occur and deal with performance issues or even deprecate things.
**This process makes use of API Encryption (key), OTA Password and WIFI credentials in secrets**.

There are 3 main files:
Factory YAML file (Which you create the .bin file with)
Main YAML file (Which will automatically be embedded within your discovered device in ESPHome)
Remote_package YAML file (Where you have all the details of all your sensors)

**Steps to follow to flash the bin (Remember to change the folowing urls to YOUR urls):**
1. Fork this repository
2. Add (or make sure you already have) the following 3lines in secrets file
wifi_ssid: "REPLACETHISWITHYOURWIFISSID"
wifi_password: "REPLACETHISWITHYOURWIFIPASSWORD"
api_encryption_key_ap_password_ota_password: "REPLACETHISWITHAA32BYTEBASE64ENCODEDSTRING"
-You can get a unique key [HERE](https://esphome.io/components/api/#configuration-variables)
4. Add a "New Device" in ESPHome
5. Select "New Device Setup"
6. Give it any name
7. Select your Device type (the current setup is for ESP32 - not variations)
8. Skip the Installation and "Edit" the yaml to include ONLY these 2 lines
```
packages:
  remote_package_shorthand: github://djgenesis/esp32-multisensor-secrets/factory.yaml@main
```
5. Click Install
6. Select "Plug into this Computer"
7. After the compilation of the bin file, download it and open https://web.esphome.io/?dashboard_install
8. Connect your device. here you might need to download and install some drivers.
9. Install the downloaded bin file. You might need to hold pressing a button of ESP32 for some seconds. If so do it before selecting Install and release after you see "Erasing". Wait until successfull installation.

**Steps to follow to add the device in ESPHome and Home Assistant (ie. End User):**

10. Head to ESPHome. After some seconds ESPHome should show it as "Discovered".
11. "Take Control" of the device.
12. Select "Update All" to ensure that updating also works. IF anything fails first click "Clean All", close popup and again "Update All".   
13. Head to HHome Assistant -> Settings - > Devices. You should see the sensor appear there as well.
14. Click "Add" and select and Area

**Congratulations! Thats it!**
