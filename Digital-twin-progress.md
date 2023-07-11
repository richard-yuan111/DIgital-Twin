# DIgital-Twin-Progress

Progress for the first semester.

## Step 1: Environment Setup

Operating System: Ubuntu 20.04

### CARLA

Carla: CARLA-0.9.13

### ROS

ROS-Noetic

### CARLA-ROS-Bridge

Install with source repository in Anaconda Environment:

Use Conda to do the package management:

1. ```bash
   conda create -n deepblue python=3.7
   ```

2. ```bash
   source activate deepblue
   ```

Create a catkin workspace:

3. ```bash
   mkdir -p ~/carla-ros-bridge/catkin_ws/src
   ```

Clone the ROS Bridge repository and submodules:

4. ```bash
   cd ~/carla-ros-bridge
   git clone --recurse-submodules https://github.com/carla-simulator/ros-bridge.git catkin_ws/src/ros-bridge
   ```

Set up the ROS environment according to the ROS version you have installed:

5. ```bash
   source /opt/ros/noetic/setup.bash
   ```

Install the required ros-dependencies:

6. ```bash
   cd catkin_ws
   rosdep update
   rosdep install --from-paths src --ignore-src -r
   ```

Use Conda install commands to install missing packages (like transforms3d) from the resdep install step.

Build the ROS bridge: 

7. ```bash
   catkin_make 
   SET(ENV{PYTHONPATH} "/the/path/you/want") 
   # due to the use of conda, specifying the python path (to CARLA Python Path) for catkin_make
   ```

For the catkin_make step, either use conda deactivate to withdraw in advance, or specify the python root while make.



## Step 2: Test the ROS Bridge

Start a CARLA server according to the installation method used to install CARLA:

1. ```bash
   source activate deepblue
   ```

Run CARLA with smaller window to reduce the burden:

2. ```bash
   cd /home/krg/Downloads/CARLA_0.9.13
   ./CarlaUE4.sh -windowed -ResX=320 -ResY240 -benchmark -fps=10
   ```

Set up source path for CARLA-ROS-Bridge:

3. ```bash
   export CARLA_ROOT=/home/krg/Downloads/CARLA_0.9.13
   export PYTHONPATH=$PYTHONPATH:$CARLA_ROOT/PythonAPI/carla/dist/carla-0.9.13-py3.7-linux-x86_64.egg:$CARLA_ROOT/PythonAPI/carla
   export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libtiff.so.5
   ```

Source:

4. ```bash
   source ~/carla-ros-bridge/catkin_ws/devel/setup.bash
   ```

Run CARLA-ROS-Bridge with ego vehicle example:

5. ```bash
   roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch
   ```

**CARLA-ROS-Bridge with ego vehicle example:**

![manule control window](/home/krg/Pictures/bridge.png)

The manual control could be utilized after pressing 'B'.



## Step 3: Sensor Data Visualization

Start an Rviz window:

1. ```bash
   rviz
   ```

In Displays/Global Options, set FIxed Frame to ego_vehicle, the ego_vehicle option could only be shown if and only if the CARLA-ROS-Bridge is successfully run with an ego vehicle as example.

Pick MarkerArray and TF from 'Add' to set up the visual environment, then add Front Camera and Lidar (PointCloud2) as sensor:

![](/home/krg/Pictures/rviz.png)

The sensor data (both lidar and front camera) corresponds to the CARLA ROS manual control window.



## Step 4: Communication between Desktops



## Step 5: DUT Involved



## Step 6: Interface from CARLA to DUT



## Step 7: Interface (Ackermann) from DUT to CARLA