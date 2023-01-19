# ros2_interview
Miniproject

## *DiffBot*

*DiffBot*, or ''Differential Mobile Robot'', is a simple mobile base with differential drive.
The robot is basically a box moving according to differential drive kinematics.
The *DiffBot* URDF files can be found in `urdf` folder of `diffbot_description` package.

1. To check that *DiffBot* description is working properly use following launch commands:
   ```
   ros2 launch diffbot_description view_robot.launch.py
   ```
   **NOTE**: Getting the following output in terminal is OK: `Warning: Invalid frame ID "odom" passed to canTransform argument target_frame - frame does not exist`.
             This happens because `joint_state_publisher_gui` node need some time to start.

1. To start *DiffBot* example open a terminal, source your ROS2-workspace and execute its launch file with:
   ```
   ros2 launch ros2_control_demo_bringup diffbot.launch.py
   ```
   The launch file loads and starts the robot hardware, controllers and opens `RViz`.
   In the starting terminal you will see a lot of output from the hardware implementation showing its internal states.
   This excessive printing is only added for demonstration. In general, printing to the terminal should be avoided as much as possible in a hardware interface implementation.

   If you can see an orange box in `RViz` everything has started properly.
   Still, to be sure, let's introspect the control system before moving *DiffBot*.

1. Check if the hardware interface loaded properly, by opening another terminal and executing:
   ```
   ros2 control list_hardware_interfaces
   ```
   You should get:
   ```
   command interfaces
        left_wheel_joint/velocity [claimed]
        right_wheel_joint/velocity [claimed]
   state interfaces
         left_wheel_joint/position
         left_wheel_joint/velocity
         right_wheel_joint/position
         right_wheel_joint/velocity
   ```
   The `[claimed]` marker on command interfaces means that a controller has access to command *DiffBot*.

1. Check if controllers are running:
   ```
   ros2 control list_controllers
   ```
   You should get:
   ```
   diffbot_base_controller[diff_drive_controller/DiffDriveController] active
   joint_state_broadcaster[joint_state_broadcaster/JointStateBroadcaster] active
   ```

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
  - RViz configuration: [diffbot.rviz](ros2_control_demo_description/diffbot_description/config/diffbot.rviz)

  - Hardware interface plugin: [diffbot_system.cpp](ros2_control_demo_hardware/src/diffbot_system.cpp)


Controllers from this demo:
  - `Joint State Broadcaster` ([`ros2_controllers` repository](https://github.com/ros-controls/ros2_controllers)): [doc](https://ros-controls.github.io/control.ros.org/ros2_controllers/joint_state_broadcaster/doc/userdoc.html)
  - `Diff Drive Controller` ([`ros2_controllers` repository](https://github.com/ros-controls/ros2_controllers)): [doc](https://ros-controls.github.io/control.ros.org/ros2_controllers/diff_drive_controller/doc/userdoc.html)
