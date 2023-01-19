# ros2_interview
Miniproject

## *DiffBot*

*DiffBot*, or ''Differential Mobile Robot'', is a simple mobile base with differential drive.
The robot is basically a box moving according to differential drive kinematics.
The *DiffBot* URDF files can be found in `urdf` folder of `ros2_bosch` package.


1. To start *DiffBot* in gazebo open a terminal, source your ROS2-workspace and execute its launch file with:
   ```
   ros2 launch ros2_bosch diffbot_gazebo.launch.py
   ```
   The launch file loads and starts the robot hardware and controllers.
 
1. To start *Command publisher node* open a terminal, source your ROS2-workspace and execute its launch file with:
   ```
   ros2 launch ros2_bosch command_node.launch.py
   ```
   The launch file loads and starts the forward and angular commade publisher nodes.

1. If everything is fine, now you can send a command to *Diff Drive Controller* using ros2 cli interface:
   ```
   ros2 topic pub --rate 30 /diffbot_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "linear:
    x: 0.7
    y: 0.0
    z: 0.0
   angular:
    x: 0.0
    y: 0.0
    z: 1.0"
    ```


Files used for this project:
  - Launch file: [diffbot.launch.py](ros2_control_demo_bringup/launch/diffbot.launch.py)
  - Controllers yaml: [diffbot_controllers.yaml](ros2_control_demo_bringup/config/diffbot_controllers.yaml)
  - URDF file: [diffbot.urdf.xacro](ros2_control_demo_description/diffbot_description/urdf/diffbot.urdf.xacro)
    - Description: [diffbot_description.urdf.xacro](ros2_control_demo_description/diffbot_description/urdf/diffbot_description.urdf.xacro)
    - `ros2_control` tag: [diffbot.ros2_control.xacro](ros2_control_demo_description/diffbot_description/ros2_control/diffbot.ros2_control.xacro)

