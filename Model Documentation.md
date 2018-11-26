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

1. prediction
  
Prediction module mainly makes decision and provide important information to Behavior Module and Trajectory Generation Module base on sensor fusion data. Here in case of how to deal with changing lane safely, we can dig out at least three important references. First, Is ego car keeps safe distance from the front car in current lane. In code, Second, Is it safe to change to left lane if need. Third, Is it safe to change to right lane if need.
  



### Conclusion
