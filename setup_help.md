# your personal computer
1. make sure you guys clone the repository to your own computer lol

2. make sure you have git, python updated too

3. run this from the repository directory

'''
source env/bin/activate
pip install -r requirements.txt
'''


'pip install opencv-python-headless' if 'python-opencv' doesn't work
# Raspberry Pi
## Set Up: Downloads

1. Get the Raspberry Pi OS (64-bit)

```bash
sudo raspi-config
# Interface Options → enable Camera
# Interface Options → enable I2C
# System Options → set locale/timezone
sudo reboot
```

2. install these too 

```bash
sudo apt-get update
sudo apt-get install -y python3-pip python3-venv python3-opencv \
    libatlas-base-dev libjpeg-dev libtiff5 libopenjp2-7 git
``'

---

