# URDF Files

## Overview
A Unified Robot Description Format (URDF) file is an XML-based file commonly used in robotics, especially the ROS ecosyustem, to mathematically define the physical and visual properties of a robot.

## Defining a Robot System
Inside a *robot* tag, you can define your robotic systems. While they are often thought about as robots, they can define whole robotic ecosystems, such as in the case of this project, where it represents a manipulator and a fixed RGBD camera sensor. Systems are fundementally made up of two components: joints and links. Links specify the physical hardware of your robot (like a chassis), whereas joints describe the nature of how links are connected. To define a link, you specify first, its offset. This offset is the transformation from the joint frame the link is attached to, to the link's frame of reference. You then define its collision properties, as well as optionally its mass, inertia, and visual properties. A special type of link is called the base link. This can be though of as the root of the transformation tree of the robot, and either can be floating (i.e. not connected by a joint to anything), or connected to the world frame.

To define a joint, you first specify the parent and child links of the joint, as well as the joint type. Next, the joint frame is specified, along with the axis of motion. The joint frame is specified as a homogenous transformation from the link frame of the parent link. 

This sequence of links and joints is commonly used by a robot state publisher to publish a transform tree with the base link as root, which is required for many robotics application. Note that if the joint is floating, typically another node will publish transforms to the base link from an *odom* frame, which is connected via a *map* frame to the world (these two frames are essentially two KF layers).

## Tags
While the above process describes the description of a robot in simple terms, there are many other tags and elements that can be used in a URDF file, such as ROS2 Control, or Gazebo. Note that as a URDF is parsed, applications will ignore unneeded tags.