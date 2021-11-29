# Episode 1 - The Blind Bot

## Introduction

If you have gone through the content of Week 0 and tried the problem, you should be familiar with the basic ideas of ROS. In addition, you should be capable of creating a simple publisher and a subscriber. If so, you are ready to face what is about to come your way. In this episode, you will see how to work in **Gazebo**, a simulator and **Rviz**, a visualizer. You will also get to play with the **TurtleBot3** in Gazebo and see the working of its sensors in Rviz.

Pictures of Gazebo, Rviz and TurtleBot3

## Gaze at Gazebo ...

## Create a World in Gazebo

## Rviz ...

## The Turtlebot3 emerges ...

## Installing Turtlebot3

For greater clarity, you may refer the following link.

[Installing Turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)

Henceforth, the **TurtleBot3** may be referred to as **bot** simply, unless specified.



## Launching TurtleBot3 in Gazebo

To summon the bot in an **empty world** in **Gazebo**, execute the following command.

```
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

Alternatively, to summon the bot in the **standard environment** in  **Gazebo**, execute the following command.

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

## Visualizing in Rviz

After launching the bot in Gazebo, to visualize it in **Rviz**, run the following command

```
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

If the bot is in the standard world, you should be able to see the point cloud representing the objects detected by the bot. Amazing !


## Moving the bot around

Using **teleop**

```
rosrun turtlebot3_teleop turtlebot3_teleop_key
```

Publishing to the topic **/cmd_vel**

Sample publisher code to make the bot move in a circular path in an anticlockwise manner
 

## Sensing the surroundings

Subscribing to the topic **/scan**

Sample subscriber code


The bot must be feeling lonely roaming all by itself. Let us bring a friend to the world.

## Summoning Multiple bots in Gazebo

## Visualizing Multiple bots in Rviz


## Way ahead

Now that you have gained the ability to write code to move the bot around and sense the surroundings, what you can do with the bot is restricted only by your imagination. 

To know more about the TurtleBot3 and explore it various capabilities 

[TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)

Additionally, one can try writing code for publishers and subscribers in different ways apart from the prescribed style, such as using **classes**. We shall leave that up to you for exploration. Have fun.

# Try it out ...

## Guiding a blind bot ...
