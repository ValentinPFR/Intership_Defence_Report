# PepperSimulation



```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt-get update && sudo apt-get install dpkg
sudo apt-get install ros-indigo-desktop-full
sudo rosdep init
rosdep update
echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt-get install python-rosinstall

```
Now we will create our catkin workspace:

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```
Now we will install all packages we need :

```
sudo apt-get install ros-indigo-pepper-robot ros-indigo-pepper-meshes ros-indigo-pepper-control ros-indigo-naoqi-dcm-driver
sudo apt-get install ros-indigo-pepper-robot ros-indigo-pepper-meshes ros-indigo-pepper-control ros-indigo-naoqi-dcm-driver
sudo apt-get install ros-indigo-pepper-dcm-bringup
sudo apt-get install ros-indigo-pepper-moveit-config
sudo apt-get install ros-indigo-moveit-ros-visualization
catkin_make
source devel/setup.bash 
roslaunch pepper_moveit_config demo.launch
```
Now if we write this the Rviz window will open :
```
roslaunch pepper_moveit_config demo.launch
```
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-12_06_38_15.png)

Then we have to install the package we need to have the Gazebo simulation working:
```
sudo apt install ros-indigo-pepper-dcm-bringup 
sudo apt install ros-indigo-pepper-control
sudo apt install ros-indigo-pepper-gazebo-plugin 
catkin_make
source devel/setup.bash
```
Now we have all we need to launch the simulation, if you want a detailed use guide of it just lokk at [here](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/How%20to%20use%20the%20bridge/README.md)

Here I will just tell you the main differencies.
So you launch gazeno with this command and start the simulation with the start button(bottom left)
And once it started you an type the second line in another terminal.
```
roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_Y20.launch
#Be sure you have start the simulation with the bottom left button before.
roslaunch pepper_moveit_config moveit_planner.launch
```
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-12_13-11-31.png)
The main difference is that you need to go Planning request --> Planning group to choose the planning group.

My VM still available on the NUC1 in the lab.
It's named "Ubuntu Trusty ros indigo".
Username:ostfalia
Password:ostfalia
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-12_13-35-19.png)

