# Installing Ardupilot and MAVProxy

### Video tutorial at https://youtu.be/wlkoq65mM2A

## Clone ArduPilot

In home directory:
```
cd ~
sudo apt-get update
sudo apt-get install git
git clone https://github.com/ArduPilot/ardupilot.git
git checkout Copter-3.6
git submodule update --init --recursive
```

## Install dependencies:
```
sudo apt install python-matplotlib python-serial python-wxgtk3.0 python-wxtools python-lxml python-scipy python-opencv ccache gawk python-pip python-pexpect
```

## Use pip (Python package installer) to install mavproxy:
```
sudo pip install future pymavlink MAVProxy
```

MAVProxy is a fully-functioning GCS for UAV’s. The intent is for a minimalist, portable and extendable GCS for any UAV supporting the MAVLink protocol (such as one using ArduPilot). For more information check out http://ardupilot.github.io/MAVProxy/html/index.html

Open `~/.bashrc` for editing:
```
gedit ~/.bashrc
```

Add these lines to end of `~/.bashrc` (the file open in the text editor):
```
export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
```

Save and close the text editor.

Reload `~/.bashrc`:
```
. ~/.bashrc
```

Run SITL (Software In The Loop) once to set params:
```
cd ~/ardupilot/ArduCopter
sim_vehicle.py -w
```
###The Techno guys channel##
```
cd ~
sudo apt-get update
sudo apt-get install git
git clone --recursive -submodules https://github.com/ArduPilot/ardupilot.git
cd ardupilot
```
#Install dependencies#
```
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
```
#configure for specific vehicle
```
./waf configure --board sitl
./waf copter
```
#Run for Arducopter
```
./Tools/autotest/sim_vehicle.py -v ArduCopter --console --map
# or
sim_vehicle.py -v ArduCopter --console --map
```
