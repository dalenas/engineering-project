# your personal computer
1. make sure you have git, python updated too

2. run this from the repository directory

3. make a folder for the repository

```
cd ~
mkdir engineering-project && cd engineering-project
```

- cd ~ goes back to root directory
- mkdir creates a folder with whatever is following as the name of the folder

4. initialize git and set up all the files/ability to push edits remotely

```
git init
git clone https://github.com/dalenas/engineering-project
```

5. set up virtual environment

```
python3 -m venv env
source env/bin/activate
```

6. download packages

```
pip install -r requirements.txt
```

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

