## Install the ROS2 build tool - Colcon

```sh
sudo apt install python3-colcon-common-extensions
```

```sh
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
```

## Create a ROS2 Workspace

```sh
mkdir my_workspace
cd my_workspace
mkdir src
colcon build
```

Then add the my_workspace/install/setup.bash to .bashrc

## Create a Python Package

```sh
cd src
ros2 pkg create my_py_pkg --build-type ament_python --dependencies rclpy
```

```sh
colcon build
```
or
```sh
colcon build --package--select my_py_pkg
```

## Create a C++ Package

```sh
ros2 pkg create my_py_pkg --build-type ament_cmake --dependencies rclcpp
```
















