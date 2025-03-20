# ros_mypy_overlay
Bundles a set of ros common messages definitions with mypy. 
## How to Use
To use this overlay, create a new overlay ros 2 workspace, clone this repo in src, build the workspace, and source the workspace before sourcing your workspace.
```
source /opt/ros/<distro>/setup.bash # Swap out your distro.
mkdir -p ~/ros2_overlays/mypy_ws/src
cd ~/ros2_overlays/mypy_ws/src
git clone --recursive git@github.com:snwu1996/ros_mypy_overlay.git
cd ~/ros2_overlays/mypy_ws
colcon build --allow-overriding \
	geometry_msgs \
	nav_msgs \
	sensor_msgs \
	sensor_msgs_py \
	std_msgs \
	std_srvs \
	visualization_msgs \
	geographic_msgs
source ~/ros2_overlays/mypy_ws/install/setup.bash
```
To add additional packages:
1. Clone or submodule add the repo into `~/ros2_overlays/mypy_ws/src` folder.
2. Include in following line
```
find_package(rosidl_generator_mypy REQUIRED)
```
in the CMakeList.txt of your `xyz_msgs` package.
3. Include the following line
```
  <build_depend>rosidl_generator_mypy</build_depend>
```
in the package.xml file of your `xyx_msgs` package.
4. rebuild the workspace and `--allow-overriding` your new msg package.
```
cd ~/ros2_overlays/mypy_ws
colcon build --allow-overriding \
	geometry_msgs \
	nav_msgs \
	sensor_msgs \
	sensor_msgs_py \
	std_msgs \
	std_srvs \
	visualization_msgs \
	geographic_msgs \
	xyz_msgs
```