## Path Planning Project

### Introduction

The goal of this project is implementing a path planner.

### Theory(Problems Description + solution +  visualized graph)  
steps: How to implement every problem, with description and code or anything else

* Problems Description
  
* Behavior Planning

* Prediction

* Trajectory Generation

### reflection(on how to generate paths)
Firstly, Thanks to the Q&A video content offered by Aaron and David. They helped me understand how to analyze trajectory planning and turn it in code. So I chose the basic code structure provided in video to add more prediction and planning functions. 

Path Planning mainly contains three modules: 

* Prediction
* Behavior Planning
* Trajectory Generation
#### prediction
  
Prediction module mainly makes decision and provide important information to Behavior Module and Trajectory Generation Module base on sensor fusion data. Here in case of how to deal with changing lane safely, we can dig out at least three important references. First, Is ego car keeps safe distance from the front car in current lane.  Second, Is it safe to change to left lane if need. Third, Is it safe to change to right lane if need. 

The implementation is by setting flag that represents wether it is safe distance or not. For example, `left_danger_flag` 
is false as default. That means the left lane of the current lane is safe to change. More concretely in this situation, the safe distance is not less than 30 meters both in front and behind us. Same meanning with `forward_danger` and `right_dange_danger`.

The prediction code snippet can be seen in lines[(*253-302*)](./src/main.cpp#L253)

#### Behavior 

This module is based on prediction and map location. The several behaviors in our case are:
  * KL
  * LCL
  * LCR

It mainly decides whether to change lane? left or right? whether to speed up or slow down? 

for our case, we wish the car drive itself as fast as possible, so if the ego car encounter a car of same lane, the first chioce is instantly changing with premise of safety. And if the situation don't allow, then it tends to speed down for not colliding with the front car. 

Another stategy is that we wish the ego car drive in the center lane if no other cars arround it.

Code can be seen in lines[(*346-366*)](./src/main.cpp#346)

With only three behaviors consider, it surely have much more to improve. Next I will include another two states, `PLCL` and `PLCR`.

#### Tajectory Generation

This module generates the trajectory based on Map Location, Prediction and Behavior. Here they include the car speed , lane state, path points, car coordinates and so on. In order to reduce high jerk or accelertaion, we could use the last two points of the previous path as starting reference. At the same time, Transformed function from Frenet to Cartian is very convient and necessary for spline calculation in calculating coordinates.

To improve the trajectory's reliability, some end points of previous trajectory are send to next trajecty. And the rest of the next trajectory are filled with coordinates by evaluating the spline and coordinates transforming.

Code of this part is in lines[(*370-479*)](./src/main.cpp*370). 


### Conclusion

The final path planner can drive well and meet the requirements.But it's not perfect. There are lot of works to do. 
* As is mentioned above, if more behavior states are considered, more good effect wil appear such as faster efficiency.
* Emergency braking parameters tuning and strategy in more complicate situation.
* Prediction. More methods to dig the sensor fusion data, such as from listed papers in course link.
* Others.

















