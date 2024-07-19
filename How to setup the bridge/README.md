# PepperSimulation




```
sudo snap install docker 
git clone https://github.com/TommyChangUMD/ros-humble-ros1-bridge-builder.git
cd ros-humble-ros1-bridge-builder
sudo docker build . -t ros-humble-ros1-bridge-builder
```
The docker build command take time don't worry it's normal (30-60 min)
```
cd ~/
sudo apt update;sudo apt upgrade
sudo apt -y install ros-humble-desktop
sudo docker run --rm ros-humble-ros1-bridge-builder | tar xvzf -
sudo apt -y install ros-humble-desktop
sudo apt install python3-rocker
xhost +
sudo  rocker --x11 --user --privileged \
         --volume /dev/shm /dev/shm --network=host -- osrf/ros:noetic-desktop \
         'bash -c "sudo apt update; sudo apt install -y tilix; tilix"'

```
Now we have our noetic terminal opened.
We just have to found the tuto to setup the simulation on Noetic.
Once it's set up we have to save the image to be able to recup this instalation when we will use the bridge again.
```
docker ps
```
We spot the ID cause we need it for the next command in our case here it's b12bddfa1a80.
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-17_15-06-30.png)

So we use the following line to save the docker image.
```
docker commit b12bddfa1a80  noetic_for_the_tutorial
```
Then you can start the docker whenever you want with this command.
```
docker run -it --rm \
    --name mon-conteneur-noetic \
    --privileged \
    --env="DISPLAY" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --volume="/dev/shm:/dev/shm" \
    --network=host \
    noetic_for_the_tutorial

```
For using the simulation you can check out this [guide](https://gitlab-fi.ostfalia.de/hcr-lab/simulation/peppersimulation/-/blob/master/Final%20part%20how%20to%20use%20the%20bridge/README.md#how-to-run-the-simulation:~:text=How%20to%20run%20the%20simulation).

Or check this [video](Bridge_installation_.mp4)
