# Episode 1 - The Blind Bot

## Launching Turtlebot3 in Gazebo

To summon the turtlebot in an **empty world**

```
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

To summon the turtlebot in the **standard environment**

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

## Visualizing the Turtlebot3 and the environment in Rviz

After launching the bot in Gazebo, run the following command

```
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

## Moving the bot around

Using **teleop**

```
rosrun turtlebot3_teleop turtlebot3_teleop_key
```

Using the topic **/cmd_vel**

Sample subscriber code
 

## Sensing the surroundings

Using the topic **/scan**


## Create a World in Gazebo

## Guiding a blind bot ...
