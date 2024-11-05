# ROS2 URDF Course

## Unit 2
2.8   URDF Materials
2.9   URDF Meshes
2.10  Joint Special Elements

2.11   Launch RVIZ2 Through A Launch File

 Execute in Webshell 1

    cd ~/ros2_ws
    colcon build --packages-select urdfbot_description
    source install/setup.bash

Execute in Webshell 2

    cd ~/ros2_ws
    source install/setup.bash
    ros2 run joint_state_publisher_gui joint_state_publisher_gui


## Unit 3:   MicroProject: Create a URDF File for Two-Wheeled Robots

3.1   MicroProject: Create a Two Wheeled Robo

    cd ~/ros2_ws/src
    ros2 pkg create --build-type ament_cmake my_box_bot_description --dependencies urdf xacro
    cd ~/ros2_ws/src/my_box_bot_description
    mkdir launch rviz urdf meshes
    touch urdf/box_bot_geometric.urdf
    touch launch/urdf_visualize_geometric.launch.py
    touch urdf/box_bot_geometric_meshes.urdf
    touch launch/urdf_visualize_meshes.launch.py

build and launch urdf pkg

    cd ~/ros2_ws
    colcon build --packages-select my_box_bot_description
    source install/setup.bash
    ros2 launch my_box_bot_description urdf_visualize_meshes.launch.py

Start the Joint State Publisher GUI to publish the joint states:

    cd ~/ros2_ws
    source install/setup.bash
    ros2 run joint_state_publisher_gui joint_state_publisher_gui

You will have to add two display elements in RVIZ2:

Robot Model
Adding display elements:

Wait until the RVIZ2 window is shown and maximize it on your screen.
To add a display, click the Add button at the bottom of the left-side panel.
You will see a list of different display types offered in the emerging window that will pop up.
Scroll down the list until you find Robot Model. Click OK. RobotModel should now appear on RVIZ's left side panel.
Configuration:

Fixed Frame: At the top of the left side panel, click on the black triangle at the left of Global Options to view/hide the Global Options details. One of the elements that will display is the Fixed Frame field with "map" as the default value. Click on the field to see a cursor blinking in the text. Set as a value, base_link, and hit 'Enter'. IT WILL NOT BE available as a drop down, you have to TYPE the value of base_link.

Robot Model: In this case, click on the black triangle at the left of Robot Model to open the details. Scroll down and confirm that Description Source is set to Topic. Then click on the empty white space at the left of Description Topic and TYPE /robot_description. Next, click on the black triangle at the left of Description Topic to view more fields. Set Reliability Policy to Reliable and Durability Policy to Transient Local.

Now, save the RVIZ configuration for later use. Go to File, Save Config As, navigate to the  package, and enter the RVIZ folder. Use urdf_vis.rviz as a file name and click 'Save'.

build and Launch 

    cd ~/ros2_ws
    colcon build --packages-select my_box_bot_description
    source install/setup.bash
    ros2 launch my_box_bot_description urdf_visualize_meshes.launch.py

Run joint_state_publisher_gui

    cd ~/ros2_ws
    source install/setup.bash
    ros2 run joint_state_publisher_gui joint_state_publisher_gui


## Unit 4:   Using URDF for Gazebo

### 4.2   Adapting a Robot Model for a Gazebo Simulation

Collisions

Inertia

    You need the inertia for Gazebo to simulate the link's moments of inertia. This allows Gazebo to simulate the torque needed to give angular acceleration to the link around a particular axis.
    There are three main moments of inertia:

    Ixx: Around the X-axis
    Iyy: Around the Y-axis
    Izz: Around the Z-axis


## Unit 5:   Moving the Robot 

### 5.2   Joint State Publisher Plugin

### 5.3   Differential Drive Plugin

### 5.4   Gazebo ROS2 Control Plugin


## Unit 6:   Sensing

### 6.1   Lidar Plugin

### 6.2   Camera Sensor Plugin

## Unit 7:   XACRO Basics

### 7.1   Basics on Using XACRO

XACRO files are an extension of URDF files. They provide a convenient way to generate URDF description elements by defining elements once and using them as many times as needed. While processing the XACRO file, each call to a macro will generate the corresponding URDF code. This simplifies the coding of robot models, reduces the amount of work required when making changes, and reduces the chance of errors, all while having a more compact description file. In addition, conditional statements let you code robot components that are generated or not, depending upon conditions evaluated at processing time. These conditions generally test values that can be defined, set, and changed from launch files. XACROs also give some tools for making basic mathematical operations inside the URDF files.

### 7.2   Manually Generating URDF Files Out of XACRO Files

    xacro box_bot.xacro > converted_box_bot_file.urdf

### 7.3   Process XACRO Files Inside Launch Files

XACRO files cannot be directly used in robot simulators as they are not compatible with the simulators. They must first be processed and converted into URDF files to use them in simulation. This conversion process can be triggered from inside a launch file when the robot model is to be spawned in a specific robot simulator such as Gazebo.

### 7.4   Properties

    With XACRO, you can define a constant value, called property, and use it as a more flexible alternative than hard-coded values. Keeping constant values as properties and referencing them when needed allows you to easily adapt your robot model without changing the same value in different places.

### 7.5   Macros

    A macro is a special XACRO element that can be used to define URDF elements that appear multiple times across the robot model. Imagine a hexapod. Instead of hard coding the same elements for each leg of the robot repeatedly, you could create a macro that defines one leg and then call that macro six times at different locations to create the six legs. If you decide you want to change the size of the legs, you would only need to change the macro that defines one leg rather than every leg's code.

### 7.6   XACRO Conditional Blocks

    XACRO provides two types of conditional blocks: the <xacro:if> block and the <xacro:unless> block. The <xacro:if> block allows you to include a section of the model only if a specified condition is true, while the <xacro:unless> block allows you to include a section of the model only if a specified condition is false.

### 7.7   Splitting Files

    This section explores how XACRO files can help you organize your robot model in different files, making it easier to understand and maintain.

### 7.8   Spawning Multiple XACRO Robot Models into Gazebo

    In Gazebo, you can create a simulation with multiple robot models, including multiple instances of the same robot model. However, creating a simulation with multiple robots in the same world is not as simple as spawning a model multiple times. This is because each robot would listen to the same command topic, publish their sensor data to the same topics, and define the same TF frames. Therefore, any ROS nodes that rely on sensor data would not function properly, and you would not be able to control the robots individually. To fix this, you must use a different namespace for each robot. You can avoid naming collisions between different topics, TF frames, and nodes using namespaces.


