# PepperSimulation


## How to run the bridge ?
For this part we assume that you already ran it once and to all the setup that we talk about before.
So you have your docker image with the done setup.
```
docker run -it --rm \
    --name mon-conteneur-noetic \
    --privileged \
    --env="DISPLAY" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --volume="/dev/shm:/dev/shm" \
    --network=host \
    noetic_pepper

```
What is doing this line ?
It will run a container with the image you saved before (in my case noetic_pepper)
Now what is the purpose of each options ?

--rm will automatically remove the container once you stopped it so it will avoid name conflict.

--name mon-conteneur-noetic It's just the name of the container you can put whatever you want that is not already used.

--privileged give the docker user high status to avoid permissions issues

--env="DISPLAY" thanks to this the container will be able to use a GUI and we need that for the simulation

--volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" mounts the host's X11 socket (/tmp/.X11-unix) into the container at the same location (/tmp/.X11-unix) with read and write permissions (rw). This allows GUI applications within the container to display their graphical interface on the host's screen.

--volume="/dev/shm:/dev/shm"
mounts the host's shared memory (/dev/shm) into the container at the same location (/dev/shm). This can improve performance for applications that use shared memory.

--network=host
uses the host's network mode for the container, meaning the container uses the host's network directly without network isolation. This may be necessary for certain use cases where the container needs to access the host's network.

noetic_pepper

Specifies the Docker image from which the container will be launched. In this case, the container will be based on the Docker image named noetic_pepper. It's my container on which I did all the installation.
Now you should have something like that.
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-11_13-32-55.png)
## How to run the simulation
Now split the terminal in two and tape thoses lines in both of them.
```
cd catkin_ws/
source devel/setup.bash 

```
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-11_13-43-36.png)

Now in one of those terminal you will launch that command line.
```
roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_Y20.launch
```
It will open Gazebo and you will click on the start button at the bottom left of the screen (in red on the next sreenshot)
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-11_13-48-10.png)

Once you have click on the start button go run that command in the second terminal.
```
roslaunch pepper_moveit_config moveit_planner.launch
```
(if you forget to launch the simulation before runningthis line Rviz will just not open)

![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-11_14-08-24.png)
So now you can plan any movment you want by choosing the planning group you want as well as the start state and the goal state.
But you can't choosean accurate trajectory here it's just random trajectory.
If you click on plan you will see a preview of the trajectory in Rviz.
If you click on Execute it will send the movment instruction to Gazebo and you will see the Gazebo Pepper robot move.
And if you click on Plan and execute you will have both the preview on Rviz and the movment on Gazebo.

If you want to set up Pepper in a particular position you have to go to the joints pane and you will have the joints correspondig at the planning group you chose before.

For example here the selected planning group is right arm so I can set several parameters to obtain the position I want.
![Terminal image](https://github.com/ValentinPFR/Intership_Defence_Report/blob/master/images/Screenshot_from_2024-07-11_15-06-27.png)

if you want a visual support here is a [video](2024-07-11_11-10-15.mkv) of me doing this tutorial.


I didn't try to do it but you can did the same on a real robot as explain in that tutorial that I use during this project: https://github.com/ros-naoqi/pepper_moveit_config
