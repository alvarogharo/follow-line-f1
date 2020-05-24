# A different triangulation approach and some optimizations
Hello!

On this blog we are going to change many things on the 3D reconstructions exercise, a new, more generic approach for triangulation without using OpenCV’s methods and more.

Let's start with the optimizations, the first one is about template matching. After many tests, I've realised that HSV is a much better color space for the template matching to work properly, so remember to convert your images before passing it to the matching functions. 

Another thing I’ve realised is that a bigger window will not always result in better matching result and if this is not correct you will have problems with the triangulations. Currently my window size is (16,16) pixels which works fine. Take also into account that OpenCV’s metrics for template matching could also be important.

Now let’s speed up the matching by minimizing the number of pixels to match. We are already only looking for patches in the epipolar line (horizontal in this case) but we could also get rid of the right part of the right image, because the object we are looking for always is going to be more to the left in the right image. With this we'll make our algorithm lighter for our CPU/GPU.

Now with let’s tackle the big one. We are going to re-implement the triangulation method by our selves. which sound difficult, but it is not as you will see. 

So, triangulation in this case, consists in searching the intersection between to lines, the 3D line between the optic center of the first camera and the matched point and this same line for the other camera with its respective optic center and image point. The problem with this is that, because of the error in the images matching, this lines will not intersect at all in most of the homolog points we’ve already found, so we have to calculate the point with less distance between this two lines.

There are multiple ways of doing that but this is the main idea:

![](http://geomalgorithms.com/Pic_d2lines.gif)

An the math approach is not as difficult as you might think, in the next link you have a pretty simple explanation of how to solve it.

https://math.stackexchange.com/questions/1993953/closest-points-between-two-lines

This new triangulation algorithm is much more visual than the OpenCV black box method and, in my case, works better than the OpenCV's approach.

Take a look to the results of this new approach:
[![](http://img.youtube.com/vi/17d5WJ5NPZw/0.jpg)](https://www.youtube.com/watch?v=17d5WJ5NPZw "Blog 2: 3D reconstruction - JdeRobot")

In the video you will also see that the plotting time is much faster, I managed to increase the plot speed of the system by twitching some sleep function in the provided code. [Here](https://github.com/JdeRobot/RoboticsAcademy/pull/544/commits/6dc29a87a3add60c85a0cab63f35cc0b774547c2) you can see the modification. This number can be changed, but be careful, if the sleep time is a very low number or 0 the 3D plotting is going to be very imprecise. In my case 0.05 was fast and precise.

Thank you for reading!






