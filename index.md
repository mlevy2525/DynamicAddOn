---
youtubeId: wKjiwAjrXgo
youtubeId2: DfP0bJOIU5g
---
### Abstract

In this paper, we address the task of interacting with dynamic environments where the changes in the environment are independent of the agent. We study this through the context of trapping a moving ball with a UR5 robotic arm. Our key contribution is an approach to utilize a static planner for dynamic tasks using a Dynamic Planning add-on; that is, if we can successfully solve a task with a static target, then our approach can solve the same task when the target is moving. Our approach has three key components: an off-the-shelf static planner, a trajectory forecasting network, and a network to predict robot's estimated time of arrival at any location. We demonstrate the generalization of our approach across environments.

{% include youtubePlayer.html id=page.youtubeId2 %}

&nbsp;
&nbsp;

### Intermediate Goals

The key behind our paper is in the introducton of an intermediate goal. We take a normal static planner, which "observes" a state and goal at each step and then lay a planner on top of it which modifies the goal location so that the planner can function for a dynamic object.

![Static vs Dynamic Planer](/img/static-vs-dynamic.png)

In order to find the intermediate goal we will need two additional tools, a Trajectory Forecasting Network and an Estimated Time of Arrival Network.

&nbsp;
&nbsp;


### Estimated Time of Arrival(ETA) Network

<div class="row">
  <div class="column">
    <img src="img/eta.png" alt="Snow" style="width:100%">
  </div>
  <div class="column">
    <p> The goal of this network is to determine how long it will take the arm from a specific position to "arrive" at a specific location on the table. To do this we use a simple Multi-Layer Perceptron Network. We discretize the ETA window of 500 time steps into 100 bins (e.g., 0-4 steps, 5-9 steps, etc.). In order to figure out which of these bins a state falls into we structure our network with 3 linear layers each with a ReLu activation network and a final layer which is also linear and outputs a probability to 100 different buckets using softmax. The output can be seen in the image below where red represents the locations the arms will reach the soonest and yellow represents the locations the arm will take the longest to reach. </p>
  </div>
</div>


&nbsp;
&nbsp;


### Trajectory Forecasting Network

<div class="row">
  <div class="column">
    <p> We opt for a faster, albeit potentially less accurate,approach than most trajectory forecasting approaches currently being used in Computer Science. We modeled our approach on the paper "Convolutional Neural Network for Trajectory Prediction." Our method requires little knowledge about the actual environment and tries to predict F steps into the future given H steps of past information, where F >> H. Therefore,we sacrifice some accuracy to gain a real-time long-horizon prediction. This is necessary because, unlike in autonomous driving, the episode happens in a very short period of time. We  cannot  wait  to  gather  a  lot  of  prior  experience.  In  ourspecific  example,  we  use 24 steps  of  prior  information  to predict 300 steps of future information.  </p>
  </div>
    <div class="column">
    <img src="img/static.gif" alt="Snow" style="width:100%">
  </div>
</div>


### Dynamic Planner
We now take these tools and combine them to create our full dynamic planner.

##### Finding Interest Points

##### Selecting the Intermediate Goal

![Panel 2/3](/img/panel_2_3.png)

##### Replannning

{% include youtubePlayer.html id=page.youtubeId %}

