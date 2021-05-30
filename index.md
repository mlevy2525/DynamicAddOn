---
youtubeId: wKjiwAjrXgo
youtubeId2: DfP0bJOIU5g
---

In this paper, we address the task of interacting with dynamic environments where the changes in the environment are independent of the agent. We study this through the context of trapping a moving ball with a UR5 robotic arm. Our key contribution is an approach to utilize a static planner for dynamic tasks using a Dynamic Planning add-on; that is, if we can successfully solve a task with a static target, then our approach can solve the same task when the target is moving. Our approach has three key components: an off-the-shelf static planner, a trajectory forecasting network, and a network to predict robot's estimated time of arrival at any location. We demonstrate the generalization of our approach across environments.

{% include youtubePlayer.html id=page.youtubeId2 %}

The key behind our paper is in the introducton of an intermediate goal. We take a normal static planner, which "observes" a state and goal at each step and then lay a planner on top of it which modifies the goal location so that the planner can function for a dynamic object.

![Sicherung vorbereiten](/img/static-vs-dynamic.png)

{% include youtubePlayer.html id=page.youtubeId %}

