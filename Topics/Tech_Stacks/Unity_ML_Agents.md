# Introduction to Unity's ML-Agents Toolkit

Unity's ML-Agents Toolkit, or simply ML Agents, is a package that provides a simple and intuitive way to develop agents capable of interacting with both 2D and 3D environments in Unity. It is a project that aims to bring machine learning together with the many environments that can be easily developed in Unity, and provide an easy and accessible way for game developers to work with machine learning.

In this introductory tutorial, we will explore the basics of reinforcement learning with an example built completely from scratch.

# Installation Guide
Before installing Unity's ML-Agents package, ensure that you installed the following:

[Unity 2022.3 or Later](https://unity3d.com/get-unity/download)

[Python 3.10.12 or Higher](https://www.python.org/downloads/)

PyTorch, it is recommended that you create a virtual environment to avoid conflicts with any existing packages.

```pip3 install torch~=1.13.1 -f https://download.pytorch.org/whl/torch_stable.html```

ML Agents Python Package, once again, install in a virtual environment.

```pip3 install ./ml-agents-envs```

```pip3 install ./ml-agents```

Finally, within Unity's Package Manager, find and install the ```com.unity.ml-agents``` package.

# What is Reinforcement Learning?

In this tutorial we will use Unity's ML-Agents Toolkit to explore the basics of reinforcement learning. Reinforcement Learning is a form of machine learning where an agent will learn to make decisions by interacting with an environment. Based on the actions it performs, it will receive a reward that indicates how well it performed. Over time, the goal of the agent is to learn a strategy that maximizes the reward it receives.

In order to do so, our agent will follow a simple cycle of 3 steps. It will first collect an observation from the environment. Using this information collected, it will perfmr an action. Finally, based on this action, we will give the agent a reward.

Our agent will attempt to learn a strategy that will maximize the reward it receives over time.


# Setting up the Environment

In this step by step tutorial, we will learn how to create a simple environment in which we are able to train an agent to play a simple game. The basic setup I will use to introduce the concepts of reinforcement learning will involve an **Agent**, and **two rewards** of varying sizes. 

<img src="https://raw.githubusercontent.com/Dismany0/misc_images/main/CSC301%20Assignment%202/Screenshot%202023-11-26%20012237.png" height="500"/>

In my setup, I have currently created a floor, an Agent, and 2 rewards.

They are positioned along a straight line. Our environment will involve the agent being able to perform 3 actions, moving left, moving right, or doing nothing at all. Hopefully, we will be able to train this agent to move towards the larger value.

Finally, to finish this section, create a C# script and attach it to your agent object. I have named the script ```BiggerRewardAgent.cs```, but feel free to change the name to anything you'd like.

# Actions

Now that our environment is set up, we will assign actions that our agent is able to perform. Begin by opening the ```CollectRewardAgent.cs``` script with any text editor you would like, such as Visual Studio or Visual Studio Code. We will begin by changing our MonoBehaviour into a Agent class. Make the following imports:

```
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;
```

We will also removing the ```Update()``` and ```Start()``` functions, and add the following overrides:

```public override void OnEpisodeBegin()```

```public override void CollectObservations(VectorSensor sensor)```

```public override void OnActionReceived(ActionBuffers actions)```

```public void OnTriggerEnter(Collider other)```

In the following few sections, we will go through and explain each of these functions in detail. We will first begin with ```OnActionReceieved()```

Unlike us, our agent is only able to play through making actions through numbers. These numbers will be given through the ActionBuffer. As specified before, we want our agent to be able to move left, right, and stand still. We will accomplish this by assigning each action a number. We begin by obtaining the action from DiscreteActions, or integer actions. We will set up where our AI gets these DiscreteActions later in our observations section.

```
public override void OnActionReceived(ActionBuffers actions)
    {
        int action = actions.DiscreteActions[0];
        switch (action)
        {
            case 0:
                transform.Translate(Vector3.left * Time.deltaTime);
                break;
            case 1:
                transform.Translate(Vector3.right * Time.deltaTime);
                break;
            case 2:
                break;
        }
    }
```
While it might make sense for us to assign case 0 to moving left, and either case 1 or 2 to moving right, the agent does not have any context to what each number means. This means that any number can be assigned to any action, and they will all be treated equally by our agent.

Now that our agent is capable of making moves, we will now make it able to make observations.

# Observations

In order for our agent to learn from its environment, it must be able to gather information from its environment. As our agent only needs to solve a very simple problem, we will give it some very simple information. To solve this problem, it should be able to observe its own position, and the position of both rewards.

To make things easier, we should add a reference to both rewards at the start of our agent class

```
public class CollectRewardAgent : Agent
{
    public GameObject rewardSmall;
    public GameObject rewardLarge;
    ...
```

This will allow us to easily access the position of both reward objects as well. To add an observation, we simply go under the CollectObservations function and call ```Sensor.AddObservation()```. We would like to add the x value of all 3 positions, as our agent will only be capable of moving along the x axis. 

```
public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(rewardSmall.transform.localPosition.x);
        sensor.AddObservation(rewardLarge.transform.localPosition.x);
        sensor.AddObservation(transform.localPosition.x);
    }
```

Here we are adding the local positions of all 3 objects. I use local position here so that if we move our training setup around, everything stays functional. However, you can adjust this depending on how your training setup may look like.

Our agent is now able to observe the world around it, as well as make movements left or right. The only thing left to do is to assign a reward function to tell our agent how well it is currently doing.
# Rewards

Now to assign a reward, this process will differ depending on what you want to train your agent to do. For our scenario, it is sufficient to give the agent a reward when it touches a reward. We will accomplish this with Unity's ```OnTriggerEnter()``` function.

```
public void OnTriggerEnter(Collider other)
    {
        if (other.gameObject == rewardSmall)
        {
            SetReward(1f);
        }
        if (other.gameObject == rewardLarge)
        {
            SetReward(10f);       
        }
        EndEpisode();
    }
```

From anywhere in Unity, we are able to assign rewards to our agent using the functions ```SetReward()``` and ```AddReward()```. For our purposes, we will set a reward when the agent collides with another object, in this case, either the small or large reward. While the amount you assign to each reward is arbitrary, they should be similar relative to each other. If the rewards are too close to each other, the agent might not learn effectively. Play with your values to find an optimal value.

Something you might have noticed is the ```EndEpisode()``` after we assign the reward. This means that we want our iteration of training to stop when our agent gets its reward, so that it can start training all over again. In order to do so, we have one last function we should call.

```
public override void OnEpisodeBegin()
    {
        transform.position = new Vector3(0, 1, 0);

        int rand = Random.Range(0, 2);
        if (rand == 0)
        {
            rewardSmall.transform.position = new Vector3(5, 1, 0);
            rewardLarge.transform.position = new Vector3(-5, 1, 0);
        }
        else
        {
            rewardSmall.transform.position = new Vector3(-5, 1, 0);
            rewardLarge.transform.position = new Vector3(5, 1, 0);
        }
    }
```

After each iteration, we want to reset our training environment. We can accomplish this by resetting the positions of each object when our training episode begins. This simply resets the position of my agent back to its starting location, and randomly assigns the rewards to place either the smaller or larger reward on either side. Feel free to adjust these values to match your training set up.

# Training

And with that, our setup is almost ready for training. Head to the inspector of our Agent. Observe the behavior parameters. There are 2 values that we should change. Feel free to assign a name to this behaviour if you would like to.

<img src="https://raw.githubusercontent.com/Dismany0/misc_images/main/CSC301%20Assignment%202/Screenshot%202023-11-26%20025032.png" height="500"/>

Our **Vector Observation** should determine the amount of observations our agent is able to make. This should match the amount of observations we gave it in our prior example, which is 3. If your training set up differs, make sure to assign the number of observations correctly.

Next, under the **Actions** section, we want to set the number of Discrete Branches to 1. This is where we are making our observations. Next, we want to set the size of our branch to 3. This should correspond to the number of possible actions our agent is able to make. As our agent is only able to move left, right, and stay still, the size of our action space is 3, as we assigned in the Actions section above.

<img src="https://raw.githubusercontent.com/Dismany0/misc_images/main/CSC301%20Assignment%202/Screenshot%202023-11-26%20031918.png" height="500"/>

The final step is to add a Decision Requester. The only parameter here is how often our agent will make an action. Feel free to play with this value.

With that, we can begin training our agent.
We can do so by opening a terminal and activating our virtual environment where we previously installed ML-Agents. To begin training, we will run 

```mlagents-learn --run-id="YOUR RUN ID HERE"```

Replacing with your own run ID. This ID could be anything that helps you identify a session of training. 

For additional parameters, run ```mlagents-learn --help``` to view them all.

Annnnnnnnd voila!

<img src="https://github.com/Dismany0/misc_images/blob/main/CSC301%20Assignment%202/ezgif.com-video-to-gif%20(3).gif?raw=true" height="500"/>

You've just learned how to train your first agent in Unity! While the agent might not appear very smart at first, it should eventually learn that moving towards the larger reward is much more rewarding than the smaller one. Over time, you should expect to see the average reward, provided every few minutes in the terminal, to increase.

Feel free to make your own adjustments or create your own training environment. Fun additions you could try to build off of this example can include
- Movement along a 2d square instead of a line
- A penalty for taking a long time to reach a reward
- Additional obstacles your agent must avoid

Feel free to explore both on your own, and with Unity's [official documentation](https://unity-technologies.github.io/ml-agents/ML-Agents-Toolkit-Documentation/) and the [ML-Agents Repo](https://github.com/Unity-Technologies/ml-agents).
