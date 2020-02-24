# Getting started
Hi!

Today I'm going to explain you how to conquer the first lap on the follow line project. Not only completing it but doing it kinda "fast". So... Let's start!

On this follow line project we have a simple communication interface with the F1 car, this is, we can access the car's images and we can set linear and angular speeds. This time, I decided to maintain the linear speed constant to simplify our first task.

The first way to tackle this problem is implementing a [PID controller](https://www.youtube.com/watch?v=wkfEZmsQqiA) to control the angular speed for our car to be able to turn. To simplify it even more I will only implement the PD part, because right now the integral is not mandatory for good results.

The error fed to the PD controller is going to be measured as the distance between the current position of the redline in the horizon and the "optimal" position which is the center of the screen.

To do this I've thresholded the image for the redline to show up. After this, I've set the horizon height empirically at ~260px and created a height window to improve the robustness of the system. With this, I've computed the x position in pixels for the redline points inside the window, got the median of this positions, round the value and used it to calculate the error with the center of the screen.

After all this, the only thing left was to set the Kp and Kd constants to the desired values, this values are obtained experimentally. Depending on how the error is computed this constants will need to be positive or negative for the car to steer in the right direction.

This implementation is minimal but I've managed to complete a lap in approximately 36 secs. Here you have a short and accelerated video of my car implementation.
[![](http://img.youtube.com/vi/BIow3qinfL0/0.jpg)](http://www.youtube.com/watch?v=BIow3qinfL0 "Blog 1: Follow Line - JdeRobot")

The main disadvantage of this approach is that the car doesn't goes over the line on the turns. The next step for solving this issue is to detect whether we are on a straight line or a turn, and create two different controllers for each state.

With this simple implementation we already have quite a fast car, but we have to continue working on its follow-line skills, meanwhile, I encourage you to try it by yourself. 

I hope you've enjoyed it! See you next time!
