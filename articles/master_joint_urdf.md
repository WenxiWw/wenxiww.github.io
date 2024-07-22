# How to make a master joint (both revolute and prismatic) in URDF file
This is a tutorial for specifying a joint that is both prismatic and revolute in URDF file.

URDF does not provide specification for a joint that is both revolute and pismatic. Two joints cannot connect directly. Therefore, we need to make a revolute joint and a prismatic joint connected by a dummy link. 

revolute joint -- dummy link -- prismatic joint

# Example code
Code of an example joint in URDF file

Revolute joint:

```xml
<joint name="upperarm_roll_joint" type="revolute">
<origin rpy="0 0 0" xyz="0.219 0 0" />
<parent link="shoulder_lift_link" />
<child link="dummy_link" />
<axis xyz="1 0 0" />
<dynamics damping="5.0" />
<limit effort="66.18" lower="-2.251" upper="2.251" velocity="1.521" />
</joint>
```
Dummy link:

```xml
<link name="dummy_link">
</link>
```

Prismatic joint:
```xml
<joint name="upperarm_prismatic_joint" type="prismatic">
<origin rpy="0 0 0" xyz="0 0 0" />
<parent link="dummy_link" />
<child link="upperarm_roll_link" />
<axis xyz="1 0 0" />
<limit effort="60" lower="0.0" upper="0.20" velocity="0.05" /><dynamics damping="100.0" />
</joint>
```
![Visualization of the joint-link connection](/images/master_joint_urdf.png)

# Visualization

To generate the tree in pdf file:

`sudo apt-get install liburdfdom-tools
urdf_to_graphiz robot.urdf`

To visualize the urdf in RVIZ: 

`roslaunch urdf_tutorial display.launch model:=PATH_TO_URDF`



# Useful links:
http://wiki.ros.org/urdf/XML/joint

https://articulatedrobotics.xyz/tutorials/ready-for-ros/urdf/