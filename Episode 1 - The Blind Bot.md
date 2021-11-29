# Episode 1 - The Blind Bot

## Introduction

If you have gone through the content of Week 0 and tried the problem, you should be familiar with the basic ideas of ROS. In addition, you should be capable of creating a simple publisher and a subscriber. If so, you are ready to face what is about to come your way. In this episode, you will see how to work in **Gazebo**, a simulator and **Rviz**, a visualizer. You will also get to play with the **Turtlebot3** in Gazebo and see the working of its sensors in Rviz.

Pictures of Gazebo, Rviz and Turtlebot3

## Gaze at Gazebo ...

## Create a World in Gazebo

## Rviz ...

## The Turtlebot3 emerges ...

## Reference

[Reference](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)

## Launching Turtlebot3 in Gazebo

To summon the turtlebot in an **empty world**

```
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

To summon the turtlebot in the **standard environment**

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

## Visualizing in Rviz

After launching the bot in Gazebo, run the following command

```
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

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


## Guiding a blind bot ...
