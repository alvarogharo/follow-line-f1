# Improving the speeds
Hello, I haven't seen you in a while.

Today, is the day. We are going to improve lap times by creating two different controllers, one for the straight lines and one for the turns.

To do this, we need to implement some algorithm to decide whether we are in a turn or in a straight. One of the most robust implementations is using the correlation coeficient between some points with different heights in the line. This coeficient is going to be close 1 or -1 if the line is straight, and viceversa. So we should stablish empirically a threshold to decide between straight or turn. As simple as that ;).

In my case, I also created a "state machine" with some conditions to change between straight or turn controller. For the system to change from one state to another we need a specific number of frames with the oppsite state to make the controller more robust and "tweakable". In fact, the number of frames needed to change from straight to turn don't need to be necessarelly the same as the frames needed to change from turn to straight. This decision is taken because when your on straight the car need to react much faster to turn than in the complentary situation.

Once we have our straight-turn detector and our "state machine" we can move on and create a new controller for each state. On the straight controller the speed is a little bit bigger and I'm using the controller we already the developed in the [first blog](https://github.com/alvarogharo/follow-line-f1/blob/master/Blog1.md).

For the turn controller some different implementations has been tested. The first intuition, is to add the integral component to the PD controller, to make the car steer more if the acumulated error is big. Remenber that with this approach we should reset the accumulated error every so often. We could also se the position of the line close to the car, and create a combined controller with the error in the horizon and the close error. I've tested both approaches but I don't know for sure which one is better because of the inestability of the development enviroment.

This implementation can complete a lap in approximately 26 secs, 10 less than in the previous blog. Here you have a short and accelerated video.

[![](http://img.youtube.com/vi/BIow3qinfL0/0.jpg)](https://youtu.be/aAy_2ecQubA "Blog 2: Follow Line - JdeRobot")

For this new implementation, the big disadvantage is a huge number of parameters to tweak which could be modified to get even better results, but with the incosistent performance of the test enviroment is difficult to adjust properly.




