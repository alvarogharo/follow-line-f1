# First full implementation
Hi!

How is it going? I hope everyone is healthy.

Today we are going to talk about the 3D reconstruction exercise. It sounds like a pretty difficult one but that's not true at all. Let start talking about it.

On this exercise we will need to plot a cloud of 3D point calculated from a stereo pair. To do this we are going to use some opencv methods and little bit of image preprocessing.

Let's start with the images themselves, we have a left and a right image from the same picture in which we will need to match patches with certain features. To simplify this task we could user SURF, FAST or similar to get features from an image but in this case we are going to use the image edges to between both. 

To get this image borders, first we are going to apply a mean filter to both of them to avoid some minor details to get in the way. Then we can user Canny algorithm to get the edge image for both left and right.

Once we have our images prepared, we will start iterating through the pixels of the left edge image and get a neighborhood of the pixels which have are white, these are the edges. This neighborhood will act as a template to match our dot on the picture with the one on the right image, for doing this we could use SSD-like metrics or user "matchTemplate" method from opencv.

Now that we have both patches matched we only need to take the image coordinates from this to features. Take into account that both patches are should have the coordinate on vertical axis because the cameras from the robot are parallel between each other. Also, make sure that the difference in the horizontal axis make sense and it's not so large that the object will need to be almost touching the cameras. To take a reference, a difference between 20 and 50 pixels should be normal for most of the points.

We can speed up this process with multiple approaches but that will be covered in the next blog.

Now let's go to the tricky part. We now need to triangulate the position of the pairs, I personally recommend doing that on the same loop as the template matching to avoid to loop again through the list of pairs. To triangulate this pairs the easiest way is to use "triangulatePoints" from openCV. You will only need the projection matrix which is KRT for each camera and the camera coordinates for each image. NOTE: KRT matrix is provided in the exercise but in extrinsics and intrinsics, this means, K and RT separately.

Once this is applied, you have the 3d point on homogeneous coordinates we will divide each component by the 4th one an take the 3 first components. Depending on how the method was implemented this point will need some scaling in my case about an 800 downscale works fine.

For finishing this long exercise the only thing left is to plot the 3D point, to do that I suggest to take the RGB color from the pixel from the left image. This plotting method is pretty slow and if your algorithm works fast you could experiences a considerable difference in execution time, because of this, here you have two videos, one without plotting the 3D points but doing everything else and the other one plotting the points.

Example without the 3D plot call:

[![](http://img.youtube.com/vi/h4p6nojExio/0.jpg)](https://www.youtube.com/watch?v=h4p6nojExio "Blog 1: 3D reconstruction - JdeRobot")


Example withthe 3D plot call:

[![](http://img.youtube.com/vi/MktGeuh9P_8/0.jpg)](https://www.youtube.com/watch?v=MktGeuh9P_8 "Blog 1: 3D reconstruction")

As you can see the second video is super slow, so don't worry if the plotting is very slow it is normal.

As we can also see, the algorithm works decently but it get lost on simple lines because the image of reference to search the patch has no texture at all, however in the more complicated parts like the Z cube it works nicely evendow it doesn't uses color to match the templates. On next we will solve that by matching the colored images and some more improvements.

See you soon!








