# Episode 1 - The Blind Bot

## Introduction

If you have gone through the content of Week 0 and tried the problem, you should be familiar with the basic ideas of ROS. In addition, you should be capable of creating a simple publisher and a subscriber. If so, you are ready to face what is about to come your way. In this episode, you will see how to work in **Gazebo**, a simulator and **Rviz**, a visualizer. 


<img src="Images/Gazebo.jpg" width=320 height=150> <img src="Images/Rviz.png" width=320 height=240>

You will also get to play with the **TurtleBot3** in Gazebo and see the working of its sensors in Rviz.

<img src="Images/Turtlebot3.png" width=200 height=240>

Let's begin !

## Initial preparation

Create a package ```epi1``` in ```catkin_ws```, with ```scripts```,```launch``` and ```configs``` folders.

## Gaze at Gazebo ...

### What is it ?

### Starting Gazebo

If you have successfully installed ROS , Gazebo should already be installed

Launch Gazebo by executing the following command

```
gazebo
```
Upon execution, the following screen should appear.

<img src="Images/Gazebo screen.png" width=600 height=400>


Welcome to Gazebo !

## Create a World in Gazebo

## Viziting Rviz ...

### What is it ?

Rviz is a **3D visualizer** for **ROS** that lets us view a lot about the **sensing**, **processing** and **state** of a robot.
This makes the **development** of robots easier and also enables us to **debug** more efficiently (better than looking at numbers on a terminal :P)

### What is the difference between Rviz and Gazebo ?

Rviz is a **visualizer** i.e it shows what the robot **perceives** is happening while Gazebo is a **simulator** i.e. it shows what is **actually** happening.

Consider the scenario in which we do not have physical hardware-based robots. In that case we would use a simulator like Gazebo to know what would actually happen and the data from the sensors can be visualized in a visualization tool like Rviz. In case we have physical robots, then the data from the sensors can still be visualized in Rviz, but we do not need a simulator necessarily.

### Installation

Execute the following command

```
sudo apt-get install ros-<Version>-rviz
```
Version = ```kinetic```, ```melodic```, ```noetic```

### Starting Rviz

Ensure that ```roscore``` is running in a separate tab. Then execute the following command,

```
rosrun rviz rviz
```
Upon execution, the following screen should appear.

<img src="Images/Rviz screen.png" width=600 height=400>

Welcome to Rviz !

### Basic features


1. **Displays** - These are entities that can be "displayed"/ represented/visualized in the world like **point cloud** and **robot state**

<img src="Images/Displays.png" width=200 height=400>

Using the **Add** button, we can add additional displays.

<img src="Images/Add_displays.png" width=200 height=320>


2. **Camera types** - These are ways of viewing the world from different angles and projections.

<img src="Images/Camera_types.png" width=300 height=100>

3. **Configurations** - These are combinations of displays, camera types, etc that define the overall layout of what and how the visualization is taking place in the rviz window.

### Saving and Loading configurations

### Starting Rviz through launch files

## The TurtleBot3 emerges ...

TurtleBot3 is the third version of the TurtleBot, which is a ROS standard platform robot for use in education and research. It is available in hardware form as well as in a simulated format. We shall be using the simulated format obviously.

TurtleBot3 comes in 3 different models - Burger, Waffle and Waffle-Pi

## Installing TurtleBot3

To install the TurtleBot3, execute the following command

```
sudo apt-get install ros-<ROS Version>-turtlebot3
```
ROS Version = ```kinetic```, ```melodic```, ```noetic```

After the above step, we need to set a **default TurtleBot3 Model** by executing the following command.

```
echo "export TURTLEBOT3_MODEL=<Model>" >> ~/.bashrc
```
Model = ```burger```,```waffle```,```waffle_pi```

We shall stick to ```burger``` for the time being.

Close the terminal.

For greater clarity, you may refer the following link.

[Installing Turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)

Henceforth, the **TurtleBot3** may be referred to as **bot** simply, unless specified.

Let us see the bot in action in Gazebo !

## Launching TurtleBot3 in Gazebo

To summon the bot in an **empty world** in **Gazebo**, execute the following command in a new terminal.

```
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

Upon execution, the following screen should be visible.

<img src="Images/Bot_Empty.png" width=300 height=200>

Alternatively, to summon the bot in the **standard environment** in  **Gazebo**, execute the following command.

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Upon execution, the following screen should be visible.

<img src="Images/Bot_Standard.png" width=400 height=400>

## Visualizing in Rviz

After launching the bot in Gazebo, to visualize it in **Rviz**, run the following command in a separate tab

```
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

If the bot is in the standard world, you should be able to see the **point cloud** representing the objects detected by the bot. Amazing !

<img src="Images/Bot_rviz.png" width=400 height=350>


## Moving the bot around

Let's move the bot around in the standard world in Gazebo using the ```turtlebot3_teleop``` package

The Turtlebot3 is a **differential drive** bot and its motion is described by its **linear velocity** and **angular velocity**. The ratio of the instantaneous linear velocity to the instantaneous angular velocity gives the **radius of curvature** of the arc it traverses at the instant.

On executing the command below,

```
rosrun turtlebot3_teleop turtlebot3_teleop_key
```
we get the ability to control the linear velocity and the angular velocity of the bot using the appropriate keys as displayed on the screen.

**w** - Increase linear velocity

**x** - Decrease linear veocity

**a** - Increase angular velocity

**d** - Decrease angular velocity

**s** - Stop

One might quickly realize that moving the bot with the keys is kind of annoying.

Let's see another way of moving the bot around using a publisher that will publish velocity commands to the ```/cmd_vel``` topic. For simplicity, we shall make it go with a constant speed in a circular path to give the basic idea.

#### Knowing the message type

How do we know the type of message that needs to be published into ```/cmd_vel``` ? Well, on launching the bot in Gazebo, execute the following command in a new tab

``` rostopic type /cmd_vel ```

The expected output is ```geometry_msgs/Twist```

To inspect the nature of this message type, execute the following command

``` rostopic type /cmd_vel | rosmsg show ```

The expected output is

```
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
```


Once we know the features of the message we are dealing with, we can proceed with writing the code.
Create a python file ```bot_move.py``` in the ```scripts``` folder of ```epi1``` 

```python
#! /usr/bin/env python

import rospy

# rosmsg type gives output of the form A/B
# The corresponding import statement will be 'from A.msg import B'

from geometry_msgs.msg import Twist 

def move():
    rospy.init_node('bot_move',anonymous=True)
    pub=rospy.Publisher('/cmd_vel',Twist,queue_size=10)

    r = rospy.Rate(10)

    vel_cmd = Twist()

    vel_cmd.linear.x = 0.1  #The bot's heading direction is along the x-axis in its own reference frame
    vel_cmd.angular.z = 0.5

    while not rospy.is_shutdown():
        pub.publish(vel_cmd)
        r.sleep()

if __name__=='__main__':
    try:
        move()
    except rospy.ROSInterruptException:
        pass

```
After saving the file, remember to make it executable.

On executing  ```rosrun epi1 bot_move.py``` in a different tab, the bot begins to move along a circular path. Cool !

## Sensing the surroundings

Moving around is not that great unless the bot is also aware of its surroundings, hence it becomes important to be able to utilize the data from its sensors such as **LaserScan**. Let's create a subscriber that will subscribe to the ```/scan``` topic to obtain the distances of the nearest obstacles at different angles with respect to the heading of the bot.

We can determine the message type that is being published into ```/scan``` like how it was determined for ```/cmd_vel```. 

Create a python file ```bot_sense.py``` in the ```scripts``` folder of ```epi1```

```python
#! /usr/bin/env python

import rospy
from sensor_msgs.msg import LaserScan

def read(data):
    theta_min = data.angle_min  # minimum angle in the field of detection
    theta_max = data.angle_max  # maximum angle in the field of detection
    R = data.ranges #Array containing the distances for different values of angle 
    l = len(R) #length of the array R

    # R[0] corresponds to the distance at theta_min
    # R[l-1] corresponds to the distance at theta_max
    # Intermediate entries correspond to the distances at intermediate angles

    print([R[0], R[l-1]])

if __name__=="__main__":
    rospy.init_node('bot_sense')
    rospy.Subscriber('/scan',LaserScan,read)
    rospy.spin()
    
```

    
On executing ```rosrun epi1 bot_sense.py``` in a different tab, we should be able to see a continuous feed of sensor readings on the terminal screen.

Move the bot around by running ```bot_move.py``` as well. What do you see ?

Try printing out ```theta_min```,```theta_max```,```l``` and other variables to get a better understanding of the features of the message.


At this point, the bot must be feeling lonely roaming all by itself. Let us bring a friend to the world. Even a high-functioning sociopath needs one :D 

## Summoning Multiple bots in Gazebo

## Visualizing Multiple bots in Rviz


## Way ahead

Now that you have gained the ability to write code to move the bot around and sense the surroundings, what you can do with the bot is restricted only by your imagination. 

To know more about the TurtleBot3 and explore it various capabilities like navigation and SLAM, refer to the link below

[TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)

Additionally, one can try writing code for publishers and subscribers in different ways apart from the prescribed style, such as using **classes**. We shall leave that up to you for exploration. Have fun.

# Try it out ...

## Guiding a blind bot ...
