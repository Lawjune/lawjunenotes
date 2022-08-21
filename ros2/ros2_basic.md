# Installation

## Installation Steps
https://blog.csdn.net/feimeng116/article/details/106602562?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166083151416780357298124%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166083151416780357298124&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-106602562-null-null.142^v42^pc_rank_34_2,185^v2^control&utm_term=ubuntu20.04%E5%AE%89%E8%A3%85ros2&spm=1018.2226.3001.4187

https://blog.csdn.net/qq_44490498/article/details/125812197?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166083362316781647588691%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166083362316781647588691&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-4-125812197-null-null.142^v42^pc_rank_34_2,185^v2^control&utm_term=91.189.91.38%2080&spm=1018.2226.3001.4187

https://blog.csdn.net/hgsdfghdfsd/article/details/124648677?ops_request_misc=&request_id=&biz_id=102&utm_term=ubuntu20.04%E5%AE%89%E8%A3%85ros2&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-124648677.nonecase&spm=1018.2226.3001.4187

## vs code plugins
- c++
- python 
- cmakee

```sh
sudo apt install python3-pip
```

## Set up environment

```sh
zen@zan-ws:/opt/ros/foxy$ ls
bin      lib               _local_setup_util.py  setup.bash  share
cmake    local_setup.bash  local_setup.zsh       setup.sh    src
include  local_setup.sh    opt                   setup.zsh   tools
```

```sh
gedit ~/.bashrc
```
Then add the following line into `~/.bashrc`

## Launch a ROS2 program

```sh
ros2 -h
usage: ros2 [-h]
            Call `ros2 <command> -h` for more detailed usage. ...

ros2 is an extensible command-line tool for ROS 2.

optional arguments:
  -h, --help            show this help message and exit

Commands:
  action     Various action related sub-commands
  bag        Various rosbag related sub-commands
  component  Various component related sub-commands
  daemon     Various daemon related sub-commands
  doctor     Check ROS setup and other potential issues
  interface  Show information about ROS interfaces
  launch     Run a launch file
  lifecycle  Various lifecycle related sub-commands
  multicast  Various multicast related sub-commands
  node       Various node related sub-commands
  param      Various param related sub-commands
  pkg        Various package related sub-commands
  run        Run a package specific executable
  security   Various security related sub-commands
  service    Various service related sub-commands
  topic      Various topic related sub-commands
  wtf        Use `wtf` as alias to `doctor`

  Call `ros2 <command> -h` for more detailed usage.
  ```

  ```sh
  ros2 run demo_nodes_cpp talker
  ```
# Write Your First ROS2 Program

## Install the ROS2 build tool - Colcon

```sh
sudo apt install python3-colcon-common-extensions
```

```sh
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
```

## Create a ROS2 Workspace

```sh
mkdir workspace
cd workspace
mkdir src
colcon build
```

Then add the workspace/install/setup.bash to .bashrc

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
ros2 pkg create my_cpp_pkg --build-type ament_cmake --dependencies rclcpp
```

Comment the C99 Setting
```sh
# Default to C99
# if(NOT CMAKE_C_STANDARD)
#   set(CMAKE_C_STANDARD 99)
# endif()
```

## ROS2 - Nodes

- **Subprograms in your applicaiton, responsible for one thing.**
- **Combined into a graph.**
- **Communicate with each other through topics, services and parameters.**

***Benefits:***
- *Reduce code complexity*
- *Fault tolerance*
- *Can be written in Python, C++, ...*

## Writing a Python Node -- Minimal Codes

Create `my_first_node.py` file in `workspace/src/my_py_pkg/my_py_pkg`

```py
#! /usr/bin/env python3
import rclpy
from rclpy.node import Node


def main(args=None):
    rclpy.init(args=args)
    node = Node("py_test")
    node.get_logger().info("Hello ROS2...")
    rclpy.spin(node)
    rclpy.shutdown()


if __name__ == "__main__":
    main()
```

```sh
zen@zan-ws:~/Projects/ros2/workspace/src/my_py_pkg/my_py_pkg$ chmod +x my_first_node.py
./my_first_node.py
```

Add a new line in `setup.py` in entry_points.console_scripts
```py
...
    entry_points={
        'console_scripts': [
            "py_node = my_py_pkg.my_first_node:main"
        ],
    },
...
```

*Under workspace directory*
```sh
zen@zan-ws:~/Projects/ros2/workspace$ colcon build --packages-select my_py_pkg
`=>
Starting >>> my_py_pkg
Finished <<< my_py_pkg [1.39s]          

Summary: 1 package finished [1.68s]
```

**Quick update:
Node, before executing ./py_node,

run: "source ~/.bashrc"

to source your workspace (or else you'll have an error)**

```sh
zen@zan-ws:~/Projects/ros2/workspace/install/my_py_pkg/lib/my_py_pkg$ source ~/.bashrc
zen@zan-ws:~/Projects/ros2/workspace/install/my_py_pkg/lib/my_py_pkg$ ./py_node 
`=>
[INFO] [1660995781.087751330] [py_test]: Hello ROS2...
```

```sh
ros2 run my_py_pkg py_node
`=>
[INFO] [1660995893.176659477] [py_test]: Hello ROS2...
```

## Writing a Python Node -- OOP

```py
#! /usr/bin/env python3
import rclpy
from rclpy.node import Node


class MyNode(Node):

    def __init__(self) -> None:
        super().__init__("py_test")
        self.__counter = 0
        self.get_logger().info("Hello ROS2...")
        self.create_timer(0.5, self.timer_callback)

    def timer_callback(self):
        self.__counter += 1
        self.get_logger().info(f"Hello {self.__counter}")


def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    rclpy.shutdown()


if __name__ == "__main__":
    main()
```

## Writing a CPP Node -- Minimal Codes

`Ctrl + Shift + B` in vscode
Then find `C/C++: Edit Configuration (JSON)`

Then we'll be able to edit `c_cpp_properties.json` in `.vscode` folder.

```JSON
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/opt/ros/foxy/include"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "gnu17",
            "cppStandard": "gnu++14",
            "intelliSenseMode": "linux-gcc-x64"
        }
    ],
    "version": 4
}
```

```cpp
#include "rclcpp/rclcpp.hpp"

int main(int argc, char **argv)
{
    rclcpp::init(argc, argv);
    auto node = std::make_shared<rclcpp::Node>("cpp_test");
    RCLCPP_INFO(node->get_logger(), "Hello cpp Node...");
    rclcpp::spin(node);
    rclcpp::shutdown();
    return 0;
}
```

**Edit CMakeLists.txt as following**
```py
cmake_minimum_required(VERSION 3.5)
project(my_cpp_pkg)

# # Default to C99
# if(NOT CMAKE_C_STANDARD)
#   set(CMAKE_C_STANDARD 99)
# endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

# if(BUILD_TESTING)
#   find_package(ament_lint_auto REQUIRED)
#   # the following line skips the linter which checks for copyrights
#   # uncomment the line when a copyright and license is not present in all source files
#   #set(ament_cmake_copyright_FOUND TRUE)
#   # the following line skips cpplint (only works in a git repo)
#   # uncomment the line when this package is not in a git repo
#   #set(ament_cmake_cpplint_FOUND TRUE)
#   ament_lint_auto_find_test_dependencies()
# endif()

# Add new nodes here
add_executable(cpp_node src/my_first_node.cpp)
ament_target_dependencies(cpp_node rclcpp)

install(TARGETS
  cpp_node
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()
```

```sh
zen@zan-ws:~/Projects/ros2/workspace$ colcon build --packages-select my_cpp_pkg
`=>
Starting >>> my_cpp_pkg
Finished <<< my_cpp_pkg [2.88s]                     

Summary: 1 package finished [3.16s]
```

```sh
source ~/.bashrc
ros2 run my_cpp_pkg cpp_node
`=>
[INFO] [1660997982.224152171] [cpp_test]: Hello cpp Node...
```

## Writing a CPP Node -- OOP

```cpp
#include "rclcpp/rclcpp.hpp"

class MyNode : public rclcpp::Node
{
public:
    MyNode() : Node("cpp_test"), counter_(0)
    {
        RCLCPP_INFO(this->get_logger(), "Hello cpp Node...");
        timer_ = this->create_wall_timer(std::chrono::seconds(1),
                                         std::bind(&MyNode::timerCallback, this));
    }

private:
    void timerCallback()
    {
        counter_++;
        RCLCPP_INFO(this->get_logger(), "Hello %d", counter_);
    }

    rclcpp::TimerBase::SharedPtr timer_;
    int counter_;
};

int main(int argc, char **argv)
{
    rclcpp::init(argc, argv);
    auto node = std::make_shared<MyNode>();

    rclcpp::spin(node);
    rclcpp::shutdown();
    return 0;
}
```

## Language Libraries

[rcl] ---> [rclpy]
      ---> [rclcpp]
      ---> [rcljava]
      ---> ...


# ROS2 Tools

## Debug and Monitor Your Nodes with ROS2 CLI

```sh
ros2 run -h
`=>
usage: ros2 run [-h] [--prefix PREFIX]
                package_name executable_name ...

Run a package specific executable

positional arguments:
  package_name     Name of the ROS package
  executable_name  Name of the executable
  argv             Pass arbitrary arguments to the executable

optional arguments:
  -h, --help       show this help message and exit
  --prefix PREFIX  Prefix command, which should go before the
                   executable. Command must be wrapped in quotes if
                   it contains spaces (e.g. --prefix 'gdb -ex run
                   --args').
```

```sh
ros2 run my_py_pkg py_node 
`=>
[INFO] [1661072578.287972781] [py_test]: Hello ROS2...
[INFO] [1661072578.789656607] [py_test]: Hello 1
[INFO] [1661072579.289657930] [py_test]: Hello 2
[INFO] [1661072579.789619593] [py_test]: Hello 3
...
...
```

```sh
ros2 node list
`=>
/py_test
```

```sh
ros2 node info /py_test
`=>
/py_test
  Subscribers:

  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
  Service Servers:
    /py_test/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /py_test/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /py_test/get_parameters: rcl_interfaces/srv/GetParameters
    /py_test/list_parameters: rcl_interfaces/srv/ListParameters
    /py_test/set_parameters: rcl_interfaces/srv/SetParameters
    /py_test/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:

  Action Clients:
```

```sh
ros2 node -h
`=>
usage: ros2 node [-h]
                 Call `ros2 node <command> -h` for more detailed usage. ...

Various node related sub-commands

optional arguments:
  -h, --help            show this help message and exit

Commands:
  info  Output information about a node
  list  Output a list of available nodes

  Call `ros2 node <command> -h` for more detailed usage.
```

## Rename a Node at Runtime

## Colcon

## Rqt and rqt_graph

## Discover Turtlesim

## Activity 001






