# Report
---
I used the DDPG (Deep Deterministic Policy Gradient) extracted of ddpg-pendulum example explained in the classroom and adapted for a 20 agent, because I chose the option 2 that uses 20 different agents and this yields 20 (potentially different) scores. I will take the average of these 20 scores.
The environment is considered solved, when the average (over 100 episodes) of those average scores is at least +30.

## Environment
In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector must be a number between -1 and 1.

## Learning Algorithm
 I used the ddpg algorithm 'ddpg_agent.py' 
 
 We must take in account that when I call the function ddpg in the notebook 'Continuous_Control.ipynb' the enter parameters of this function was modified in order to adapt the requirements of this project. 
 
### Using

- n_episodes (int): maximum number of training episodes
- max_t (int): maximum number of timesteps per episode

Where
`n_episodes=300`, `max_t=1000`

NOTE: I needed to use the active_session function in order to prevent the disconection of the udacity workspace, adding inside the ddpg function the line

''''with active_session(): #To prevent the desconection of workspace''''

You must import this function from workspace_utils.py added at this repository.

This is because the training could spent more than 14 hours.

###Hyperparameters

- BUFFER_SIZE (int):  int(1e6) replay buffer size
- BATCH_SIZ (int): 1024 mini batch size
- GAMMA (float): 0.99 discount factor
- TAU (float): 1e-3  for soft update of target parameters
- LR_ACTOR (float): 1e-4 learning rate for optimizer
- LR_CRITIC (float): 1e-4 learning rate for optimizer
- WEIGHT_DECAY (float): 0 L2 weight decay
- N_LEARN_UPDATES (int): 10 number of learning updates
- N_TIME_STEPS (int): 20 every n time step do update

The main modification in this 'ddpg_agent.py' is in OUNoise parameters:

I modified 'theta=0.16' and 'sigma=0.1' following the instrunction given in the nanodegree by Alessandro Restagno in the project TIPS.

After this modifications I observed a huge improvement in the learning of my algorithm. I hadn't significative improvements when I tried to modify other parameters like bacth_size or lr_actor and lr_critic.
Neither when I tried modify the number of the layers of my 'model.py'


### Model

The model was extracted of the example provided in ddpg-pendulum of the DRLND repository and modified the number of units of the actor and the critic:

Actor ----  fc1_units=256, fc2_units=128
Critic ---- fc1_units=256, fc2_units=128

Being  ----> fc1_units (int): Number of nodes in first hidden layer
             fc2_units (int): Number of nodes in second hidden layer

## RESULTS

```
Episode 1	Average Score: 0.62
Episode 2	Average Score: 1.02
Episode 3	Average Score: 1.24
Episode 4	Average Score: 1.65
Episode 5	Average Score: 1.90
Episode 6	Average Score: 2.41
Episode 7	Average Score: 2.96
Episode 8	Average Score: 3.59
Episode 9	Average Score: 4.45
Episode 10	Average Score: 5.16
Episode 11	Average Score: 6.21
Episode 12	Average Score: 7.47
Episode 13	Average Score: 8.73
Episode 14	Average Score: 10.05
Episode 15	Average Score: 11.38
Episode 16	Average Score: 12.62
Episode 17	Average Score: 13.76
Episode 18	Average Score: 14.84
Episode 19	Average Score: 15.78
Episode 20	Average Score: 16.74
Episode 21	Average Score: 17.61
Episode 22	Average Score: 18.49
Episode 23	Average Score: 19.34
Episode 24	Average Score: 20.09
Episode 25	Average Score: 20.78
Episode 26	Average Score: 21.42
Episode 27	Average Score: 22.04
Episode 28	Average Score: 22.60
Episode 29	Average Score: 23.12
Episode 30	Average Score: 23.60
Episode 31	Average Score: 24.08
Episode 32	Average Score: 24.54
Episode 33	Average Score: 24.95
Episode 34	Average Score: 25.33
Episode 35	Average Score: 25.69
Episode 36	Average Score: 26.05
Episode 37	Average Score: 26.39
Episode 38	Average Score: 26.69
Episode 39	Average Score: 26.96
Episode 40	Average Score: 27.22
Episode 41	Average Score: 27.47
Episode 42	Average Score: 27.73
Episode 43	Average Score: 27.99
Episode 44	Average Score: 28.23
Episode 45	Average Score: 28.46
Episode 46	Average Score: 28.68
Episode 47	Average Score: 28.88
Episode 48	Average Score: 29.08
Episode 49	Average Score: 29.28
Episode 50	Average Score: 29.47
Episode 51	Average Score: 29.63
Episode 52	Average Score: 29.78
Episode 53	Average Score: 29.95
Episode 54	Average Score: 30.10

Environment solved in -46 episodes!	Average Score: 30.10
```

![](https://github.com/manuelpinar/Reinforcement-Learning-Project2-Continuous-Control/blob/master/graphic_average.png?raw=true)

### Future improvements

Following the tips offered by Alessandro Restagno in the nanodegree, other improvements that we could use is BachtNorm in the data.
Also, we could use other algorithms like Trust Region Policy Optimization (TRPO) and Truncated Natural Policy Gradient (TNPG) should achieve better performance. Other could be Proximal Policy Optimization (PPO), which has also demonstrated good performance with continuous control tasks.
