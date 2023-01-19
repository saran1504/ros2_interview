# ros2_interview
Miniproject

## *DiffBot*

*DiffBot*, or ''Differential Mobile Robot'', is a simple mobile base with differential drive.
The robot is basically a box moving according to differential drive kinematics.
The *DiffBot* URDF files can be found in `urdf` folder of `ros2_bosch` package.


1. To start *DiffBot* example open a terminal, source your ROS2-workspace and execute its launch file with:
   ```
   ros2 launch ros2_bosch diffbot.launch.py
   ```
   The launch file loads and starts the robot hardware and controllers.
 

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
   You should now see an orange box circling in `RViz`.
   Also, you should see changing states in the terminal where launch file is started.


Files used for this demos:
  - Launch file: [diffbot.launch.py](ros2_control_demo_bringup/launch/diffbot.launch.py)
  - Controllers yaml: [diffbot_controllers.yaml](ros2_control_demo_bringup/config/diffbot_controllers.yaml)
  - URDF file: [diffbot.urdf.xacro](ros2_control_demo_description/diffbot_description/urdf/diffbot.urdf.xacro)
    - Description: [diffbot_description.urdf.xacro](ros2_control_demo_description/diffbot_description/urdf/diffbot_description.urdf.xacro)
    - `ros2_control` tag: [diffbot.ros2_control.xacro](ros2_control_demo_description/diffbot_description/ros2_control/diffbot.ros2_control.xacro)


Controllers from this demo:
  - `Joint State Broadcaster` ([`ros2_controllers` repository](https://github.com/ros-controls/ros2_controllers)): [doc](https://ros-controls.github.io/control.ros.org/ros2_controllers/joint_state_broadcaster/doc/userdoc.html)
  - `Diff Drive Controller` ([`ros2_controllers` repository](https://github.com/ros-controls/ros2_controllers)): [doc](https://ros-controls.github.io/control.ros.org/ros2_controllers/diff_drive_controller/doc/userdoc.html)
