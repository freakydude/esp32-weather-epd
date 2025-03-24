# Fork of ESP32 E-Paper Weather Display

!!! Experimental !!!

## Run in WSL2 with VSCode + DevContainer + USB Access


### Windows Command or Powershell
- Get [usbidp-win](https://github.com/dorssel/usbipd-win)
  - Install it with 
    ```bat
    winget install usbipd
    ```
- Update to latest WSL2
  ```
  wsl --update
  ```

- Connect your ESP per USB/Serial
- List usb devices
  ```  
  usbipd list
  ```
  ```
  BUSID  VID:PID   DEVICE   STATE
  ...
  2-4    1a86:7522  USB-SERIAL CH340K (COM5)  Not shared
  ...
  ```
- Bind your Controller and attach to running WSL (here ID: 2-4)
  ```
  usbipd bind --busid=2-4
  usbipd attach --auto-attach --wsl --busid=2-4
  ```

### WSL2
- Your USB device should be listed
  ```
  ls -lisa  /dev/ttyUSB*
  ```
- Get Access Rights (remember, you run the platform io in a devcontainer later, so it's not your user accessing the usb device later). So for a very easy setup, just add read write permission for all users to the usb device
  ```
  sudo chmod a+rw /dev/ttyUSB0   
  ```

- Add permanent usb access rights
  ```
  sudo nano /etc/udev/rules.d/platformio.rules 
  ```
  add
  ```
  SUBSYSTEMS=="usb", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7522", GROUP="dialout", MODE="0666"
  ```


### Open the Project with vscode
- ```
  git clone ...
  cd esp32-weather-epd
  code .  
  ```
- Reopen the project in DevContainer, install the dev container vscode extension if needed

- Open the platformio folder with the platformio extension. Install the platform io extension if needed

- try to build and upload the project to your esp controller




## Original Readme [Original Readme](README.org.md)
