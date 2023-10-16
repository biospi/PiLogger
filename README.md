# PiLogger
Turn your Raspberry Pi into a datalogger. <br>
Credit:https://github.com/pimoroni/weatherhat-python <br>
Credit:https://learn.pimoroni.com/article/getting-started-with-weather-hat

## How To Use

### RaspberryPi OS and SSH access over Wi-Fi

1) Create a Raspberry Pi Image on your external SD card with **Raspberry Pi Imager** (https://www.raspberrypi.com/software/) <br>
Follow https://learn.pimoroni.com/article/getting-started-with-weather-hat up to section **INSTALLING RASPBERRY PI OS (WITH REMOTE ACCESS)**
<br>
*Note: Make sure to install Python >=3.6

### Connect to RaspberryPi and install software
Once connected via ssh with Putty for example.

1) Run to enable the Raspberry Pi I2C and SPI interfaces.
```bash
sudo raspi-config nonint do_i2c 0
sudo raspi-config nonint do_spi 0
```

2) Run
```bash
sudo apt-get install libatlas-base-dev
```

3) Clone the repository.
```bash
git clone https://github.com/biospi/WeatherPi.git
cd WeatherPi
./install.sh --unstable
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