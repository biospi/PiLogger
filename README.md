# PiLogger
Turn your Raspberry Pi into a datalogger. <br>
Credit:https://github.com/pimoroni/weatherhat-python <br>
Credit:https://learn.pimoroni.com/article/getting-started-with-weather-hat

## How To Use

### RaspberryPi OS and SSH access over Wi-Fi

Create a Raspberry Pi Image on your external SD card with **Raspberry Pi Imager** (https://www.raspberrypi.com/software/) <br>

* Select RASPBERRY PI OS(32-BIT)
<br>**In the setting panel:** 
* Enable SSH
* Set usrname and password
* Configure wifi: <br>SSID: eduroam<br>password: "your password" 

Click Write to flash the sd card. When finished pop it in the PiLogger.

### Setup Eduroam for internet acess
Connect a monitor to your PiLogger and plug in power source.
* Connect to Bristol-WiFi-Setup
* Open browser and Follow https://www.wireless.bris.ac.uk/eduroam/instructions/go-ubuntu/

After following the instruction you should have access to the internet from your Pilogger.

### Connect to Eduroam on boot automatically
To tell the Raspberry Pi to automatically connect to your WiFi network you need to edit a file called: wpa_supplicant.conf.

To open the file in nano type the following command:
```bash
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Scroll to the end of the file and add the following to the file to configure your network:
```bash
network={
   ssid="eduroam"
   psk="SecretPassWord"
}
```
_Remember to replace this with your own network name and password._
Save and close the file by pressing Ctrl+X followed by Y. At this point the Raspberry Pi should automatically connect to your network.
   
### Connect to RaspberryPi and install software
With any pc connected to eduroam ou can now connect to the PiLogger via ssh with Putty for example with the login details you setup in the first step.<br>
or you can also just continue the installation on the PiLogger GUI with a monitor by opening a new terminal window. 
<br>_*Note: SSH may not be possible over eduroam_


1) Run to enable the Raspberry Pi I2C and SPI interfaces.
```bash
sudo raspi-config nonint do_i2c 0
sudo raspi-config nonint do_spi 0
```

2) Run to install dev libraries
```bash
sudo apt-get install libatlas-base-dev
```

3) Clone the repository.
```bash
git clone https://github.com/biospi/PiLogger.git
cd PiLogger
chmod +x install.sh
sudo ./install.sh --unstable
```

4) Create python virtual environment 
```bash
python3 -m venv venv
```
5) Activate the environment
```bash
source venv/bin/activate
```
6) Install dependencies 
```bash
make environment
```

7) Test with 
```bash
python examples/basic.py
```

### Setup Launcher to start app on boot

Give the launcher script permissions with:
```bash
chmod +x /home/$USER/PiLogger/launcher.sh
```
Type in:
```bash
crontab -e
```
This will bring up a crontab window.
Select editor and add at the bottom:
<br>
**Replace fo18103 with the username you set up in step 1 (RaspberryPi OS and SSH access over Wi-Fi)** 
```bash
@reboot sleep 30; /home/fo18103/PiLogger/launcher.sh >> /home/fo18103/PiLogger/cronlog.txt 2>&1
```
Will execute main.py script on boot.
Type in to check that the cron job is active:
```bash
crontab -l
```

try it with:
```bash
sudo reboot
```

### TODO
* Deep sleep mode in between record
* Data download via SSH or other