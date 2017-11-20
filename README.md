    Student describes the effect of the P, I, D component of the PID algorithm in their implementation. Is it what you expected?

The proportional component was the first to be tuned. It oscillates the car around the center of the lane. This component alone is not enough since the proportional controller has a strong tendency to overshoot and overshooting sharply on tight curves steers the car off-road. The reason for this is that the control input is simply a proportional and symmetrical value to the Cross Track Error (CTE).

The next parameter to tune is the derivative component, which aims to dampen the overshooting nature of the proportional controller. The control signal now takes into account the derivative of the CTE. The proportional derivative controller provided good results in this project. Adding the derivative component was enough to have the car complete the track moderately fast.

Finally, the integral component addresses environments where there is a systematic bias. In this project, the effect this parameter seemed small. It was not possible to observe a significant bias on the track. However, since the track is a loop, there is only one curve to the right and the car typically is to the right of the lane center during curves to the left, the integral of the CTE "picks up" on a bias. This is most observable when the road does not curve, since the integral component will steer the car slightly towards the left of the lane center to counterbalance the perceived bias. This is also clear on the demonstration videos on the curve to the right. On the video including the integral component, the car curves closer to the outer edge of the road than when the same component is not present. That said, it also makes the curves to the left closer to the lane center. Whether it should be included merits some discussion. To optimize the performance of the car on this particular track, it should definitely be added and tuned. However, in the real world, we don't usually optimize for a track - the number of curves to the left or the right is arbitrary - and since the bias is on the track and not the car, in a real-world application the integral component would not make a significant contribution.


All in all, the behaviour of the implemented controller was in accordance to what was discussed in the lessons.


    Describe how the final hyperparameters were chosen.

I started by implementing a simple proportional controller for the speed. I tuned the proportional constant to 0.25, which did the job well enough. This controller kept a constant speed and didn't take into account the CTE for following the lane center.

Afterwards, I started by tuning a proportional controller for following the lane center. Starting with 1.0, I kept reducing this constant because the oscillation was too high. I got to a value where the car could go around the track at a very low speed. For increasing the speed, I would need a way to reduce the oscillation amplitude.

I then added the derivative component to work with a speed of 30 mph. Tuning this parameter was done by adding and not subtracting. I observed that if the derivative constant was too high, the car stopped converging to the lane center in some critical parts of the track.

Finally, I started to tune the integral component. As written above, the effect of this component seemed subtle.

After I got both PD and PID controller working, I tried tuning a little more the different paramters. I settled for a proportional value of 0.1 and a derivative value of 2.0. The integral value used in the demonstration video was 0.001. When the intral value went much above this, the PID controller seemed to behave mostly like the PD controler.


# Demonstration videos
[PID controller](https://youtu.be/2XuMIXTihU4)

[PD controller](https://youtu.be/9cQY9F8tMck)

[P controller](https://youtu.be/pCEsSdKYLis)
