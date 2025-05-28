# Installing Gazebo and ArduPilot Plugin

### Video Tutorial at https://youtu.be/m7hPyJJmWmU

## Overview 

Robot simulation is an essential tool in every roboticist's toolbox. A well-designed simulator makes it possible to rapidly test algorithms, design robots, perform regression testing, and train AI system using realistic scenarios. Gazebo offers the ability to accurately and efficiently simulate populations of robots in complex indoor and outdoor environments. At your fingertips is a robust physics engine, high-quality graphics, and convenient programmatic and graphical interfaces. Best of all, Gazebo is free with a vibrant community.

for more infromation on gazebo checkout http://gazebosim.org/

## Install Gazebo [***18.04-20.04***]

Setup your computer to accept software from http://packages.osrfoundation.org:
```
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
```

Setup keys:
```
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
```

Reload software list:
```
sudo apt update
```

Install Gazebo:
### Ubuntu [***18.04***]
```
sudo apt install gazebo9 libgazebo9-dev
```
### Ubuntu [***20.04***] (Gazebo classic = Gazebo 11)
```
sudo apt-get install gazebo11 libgazebo11-dev
```

### Ubuntu [***22.04.5***] (Gazebo Harmonic)
```
sudo apt-get install curl lsb-release gnupg

sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null

sudo apt-get update
sudo apt-get install gz-harmonic
```

for more detailed instructions for installing gazebo checkout http://gazebosim.org/tutorials?tut=install_ubuntu


## Install Gazebo plugin for APM (ArduPilot Master) %This is for Gazebo Classic:
```
cd ~
git clone https://github.com/khancyr/ardupilot_gazebo.git
cd ardupilot_gazebo
```
***Ubuntu 18.04 only*** checkout dev
```
git checkout dev
```
build and install plugin
```
mkdir build
cd build
cmake ..
make -j4
sudo make install
```
Set paths for models:
```
echo 'export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models' >> ~/.bashrc
. ~/.bashrc
```
###For Gazebo Harmonic in Ubuntu 22.04.5###
```sudo apt update
sudo apt install libgz-sim8-dev rapidjson-dev
sudo apt install libopencv-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl

mkdir -p ~/gz_ws/src
cd ~/gz_ws/src
git clone https://github.com/ArduPilot/ardupilot_gazebo.git

#Building the plugin
cd ~/gz_ws
mkdir build
cd build
cmake ../src/ardupilot_gazebo
make -j$(nproc)

#Setting environment variables. Add following lines to your ~/.bashrc to ensure Gazebo finds the plugin and models at #runtime:
export GZ_SIM_SYSTEM_PLUGIN_PATH=$HOME/gz_ws/build:$GZ_SIM_SYSTEM_PLUGIN_PATH
export GZ_SIM_RESOURCE_PATH=$HOME/gz_ws/src/ardupilot_gazebo/models:$HOME/gz_ws/src/ardupilot_gazebo/worlds:$GZ_SIM_RESOURCE_PATH

#Reload the shell
source ~/.bashrc

#Running an example
#Terminal one: start gazebo
gz sim -v4 -r iris_runway.sdf

#Terminal two: start ardupilot sitl with gazebo iris model
sim_vehicle.py -v ArduCopter -f gazebo-iris --model JSON --map --console

```
## Run Simulator

**NOTE the iris_arducopter_runway is not currently working in gazebo11. The iq_sim worlds DO work**

In one Terminal (Terminal 1), run Gazebo:
```
gazebo --verbose ~/ardupilot_gazebo/worlds/iris_arducopter_runway.world
```

In another Terminal (Terminal 2), run SITL:
```
cd ~/ardupilot/ArduCopter/
sim_vehicle.py -v ArduCopter -f gazebo-iris --console
```


