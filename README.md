This is the repository which keeps files relevant for the BWIBot v5's usage in simulation. It stores SLDParts, STL/DAE meshes, OBJ files, and more.
This README will be used as a changelog/instruction manual for launching the urdfs in RViz and Gazebo environments.
This repository does not yet contain the actual rospack for utilizing the v5.

Having the v5 package installed, here's how to launch the different URDF files in Gazebo and RViz respectively. Right now, we are using the limited joint version
of the ur5.

First, make sure to perform the following steps:
1) cd into the catkin_ws_bwi workspace
2) source devel/setup.bash

**IMPORTANT**
Any changes made to the robot should be made in the .xacro file.

Gazebo:
Launching the v5 in Gazebo utilizes the ur5_joint_limited_robot.urdf.xacro file, and the appropriate launch file is ur5_joint_limited.launch.

1) roslaunch v5_asm ur5_joint_limited.launch

This should open up a Gazebo window with the v5's base and arm attached. The arm could be moved with the ur5 moveit config, but we still have to configure
appropriate bounding boxes before this function can be properly utilized without breaking the simulation.

RViz:
Launching the v5 in RViz utilizes the ur5_joint_limited_robot.urdf file, and the appropriate launch file is display.launch

1) roslaunch v5_asm display.launch

This should open up an RViz window with the v5's base and arm attached, as well as a separate joint_state_publisher_gui which allows you to move the arm.
Right now, collision isn't configured properly so the arm can clip directly through any solid objects in the simulation. We must fix this eventually.

**IMPORTANT**
If you make any changes to the ur5_joint_limited_robot.urdf.xacro file (add any extra robot parts, etc.) PLEASE make sure to update the ur5_joint_limited_robot.urdf
file by performing the following steps. This is necessary in order to launch the file in RViz - these steps must be followed as modifying the .xacro file does not
directly update the .urdf file. Changes to the .xacro file only affect launching the file in Gazebo.

1) (Optionally, make a copy) Delete the ur5_joint_limited_robot.urdf file. 
2) Run the following command in the catkin_ws_bwi/src/segbot/v5_asm/urdf directory:

  rosrun xacro xacro -o ur5_joint_limited_robot.urdf ur5_joint_limited_robot.urdf.xacro

This will create a new ur5_joint_limited_robot.urdf file, which can be launched directly through the display.launch file and will update with any changes made
to the .xacro file.
