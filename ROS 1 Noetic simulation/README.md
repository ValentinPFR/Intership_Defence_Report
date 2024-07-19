# PepperSimulation



Now we will create our catkin workspace:

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```
It's basically the same as for Indigo but packages are not available with apt on noetic so we need to install them manually.
We will use a .rosinstall file to do it.
```
sudo apt install git
#create a .rosinstall file in the src folder
cd ~/catkin_ws/
cd src/
nano .rosinstall

- git:
    local-name: pepper_robot
    uri: https://github.com/ros-naoqi/pepper_robot.git
    version: master
- git:
    local-name: pepper_meshes
    uri: https://github.com/ros-naoqi/pepper_meshes.git
    version: master

- git:
    local-name: pepper_dcm_robot
    uri: https://github.com/ros-naoqi/pepper_dcm_robot.git
    version: master
- git:
    local-name: pepper_moveit_config
    uri: https://github.com/ros-naoqi/pepper_moveit_config.git
    version: master
    
- git:
    local-name: pepper_virtual
    uri: https://github.com/ros-naoqi/pepper_virtual.git
    version: master

#ctrl x to close the file
cd ..
wstool update -t src
catkin_make
sudo apt-get install ros-noetic-moveit
```
Now we have to run the the pepper_meshes installation file. 
Normally we just have to go to the devel space ane run make pepper_meshes_meshes or pepper_meshes.
```
cd ~/catkin_ws/
cd devel/
make pepper_meshes_meshes
# or make pepper_meshes
```
If we encountered an issue with that like make file not found we can do it maually:
```
cd /catkin_ws/devel/tmp
./installer.run 
```
It will run the pepper_meshes installatiuon file manually.
We will have a pop up asking for the installation path now:
Be careful it's important to put it in the catkin_ws/src/pepper_meshes
Like this:
Now if we write this the Rviz window will open :
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-12_16-25-43.png)

```
sudo apt-get install ros-noetic-gazebo-ros-pkgs
source devel/setup.bash 
roslaunch pepper_moveit_config demo.launch
```
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-12_06_38_15.png)
To launch the gazebo simulation type this line:
```
roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_Y20.launch
#Don't forget to source before
```
If Pepper's arms are falling down in Gazebo try this procedure to fix it:

If they are not just skip that part.
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/test.png)

```
sudo rosdep init
sudo rm /etc/ros/rosdep/sources.list.d/20-default.list
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src -r -y
source devel/setup.bash 
roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_Y20.launch
 ```
Once the gazebo simulation is launched just click on the start button at the bottom left of the screen.
Then open another terminal :

```
cd catkin_ws/
source devel/setup.bash
roslaunch pepper_moveit_config moveit_planner.launch
```
To understand in details how the simulation works just check the 'How to run the simulation' part of this [tutorial](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/How%20to%20use%20the%20bridge/README.md#how-to-run-the-simulation)
