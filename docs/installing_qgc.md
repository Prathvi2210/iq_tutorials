# Intalling QGroundControl 

### Video tutorial (18.04) at https://youtu.be/qLQQbhKDQ6M

### Video Tutorial (20.04) at https://youtu.be/1FpJvUVPxL0

## Overview 

QGroundControl provides full flight control and vehicle setup for PX4 or ArduPilot powered vehicles. It provides easy and straightforward usage for beginners, while still delivering high end feature support for experienced users.

### Key Features:

- Full setup/configuration of ArduPilot and PX4 Pro powered vehicles.
- Flight support for vehicles running PX4 and ArduPilot (or any other autopilot that communicates using the MAVLink protocol).
- Mission planning for autonomous flight.
- Flight map display showing vehicle position, flight track, waypoints and vehicle instruments.
- Video streaming with instrument display overlays.
- Support for managing multiple vehicles.
- QGC runs on Windows, OS X, Linux platforms, iOS and Android devices.

for more detailed information please visit http://qgroundcontrol.com/

## Install QGroundControl for Ubuntu Linux 16.04 LTS or later:

Add current user accout to dialout group and remove modemmanager
```
sudo usermod -a -G dialout $USER
sudo apt-get remove modemmanager
```

Download QGroundControl.AppImage 
```
wget https://s3-us-west-2.amazonaws.com/qgroundcontrol/latest/QGroundControl.AppImage
```
Change permissions and run 
```
chmod +x ./QGroundControl.AppImage
```
Runninf the software
```
sudo apt update
sudo apt install fuse
sudo apt install libfuse2

sudo apt install gstreamer1.0-gl
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav

#xcb libraries
sudo apt install --reinstall libxcb-xinerama0 libx11-xcb1 libxcb1 libxcb-render0 libxcb-shape0 libxcb-randr0 libxcb-glx0

#Qt libraries
sudo apt install qtbase5-dev qt5-qmake qtbase5-dev-tools
sudo apt install qtbase5-dev qt5-qmake qtbase5-dev-tools libxcb-xinerama0 libx11-xcb1 libxcb1 libxcb-render0 libxcb-shape0 libxcb-randr0 libxcb-glx0

#Setting env. variable for debugging and more detailed error messages
export QT_DEBUG_PLUGINS=1

./QGroundControl.AppImage  (or double click)
```

## Run SITL and connect with Q Ground

```
cd ~/ardupilot/ArduCopter/
sim_vehicle.py
```

