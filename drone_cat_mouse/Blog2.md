# Using the second camera and more
Hi!

Lets continue with the second camera! The implementation for this ventral camera is almost the same as the frontal one, the only difference is taking the other image and change the axis in which each velocity is applied and calculated.

With this in mind the only thing we are going to do is applying the x on the z velocity, the y on the y and finally the z on the x. And also create a new reference area for the z movement to be correctly adapted. That's it.

Then we create new constant variables for the other image to manage independently both controllers and the drone should works as intended. Easy, right?

Well, this not everything you need now we need to implement an state machine to change between the to controller depending on which camera is catching the drone. For doing this we only need to count the number of blobs on each image, the one with more than 0 blob is the winner. This works because the cameras does not overlap, which will avoid possible blobs on both cameras at the same time.

But, what happens if there is no blob in any camera?. Well, we need to create a third state, the search state.

For this state one of the simplest approach, is to make the drone go up and rotate slowly, this will cover some space of the environment but some other path could work better.

Take a look to the results of this approach:

[![](http://img.youtube.com/vi/88LXdC005Rk/0.jpg)](https://www.youtube.com/watch?v=88LXdC005Rk "Blog 2: Drone cat mouse 2 - JdeRobot")

The search state:

[![](http://img.youtube.com/vi/WhprPkKQkUc/0.jpg)](https://www.youtube.com/watch?v=WhprPkKQkUc "Blog 2: Drone cat mouse 3 - JdeRobot")

Thank you for tunning in. See you in the next one!






