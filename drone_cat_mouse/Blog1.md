# Getting started
Hello!

Today we are continuing with a new project the "drone cat and mouse". On this exercise we will need to implement again some PDI logic in a different environment, in this case controlling a drone.

This time we also have a red drone which we will need to follow without colliding with it. This drone has to cameras, for now we will only implement the frontal one.

First of all, as we already now, we are going to threshold the image to get a mask in which only the red drone will be highlighted.

Then we need to think about the different variables we need to control for the drone to move. This drone has four variables to control related to x, y and z linear velocities and angular velocity in the z axis.

For this approach we are only using three of this axis because the rotation in z and the linear velocity in y most of the time can be swapped.

Then lets create a PD controller with a 3D vector instead of scalars. Each of the components of the resultant vector will create our final velocity.

But how do we calculate the error for each axis? Ok, let's start with the easiest one. For the dorne to be able to move in y and z axis we will need to get the center of mass of the drone in the image and subtract it from the center of these image. With that we will have the error for this to axis.

For the x axis in this case we will need to get the area of the red drone in our image and set a reference area (related to the distance to the drone) from which we will subtract the current area. And that's it!

Of course for each of this 3 dimensions we will need the constants "P" and "D" to tune the drone behaviour.

Here you have some example of the current state of the controller working:[![](http://img.youtube.com/vi/BIow3qinfL0/0.jpg)](http://www.youtube.com/watch?v=BIow3qinfL0 "Blog 1: Follow Line - JdeRobot")

NOTE: As I said before the y axis velocity value can be changed to the rotation in z axis. Applying this velocity as rotation could give more robust results.

