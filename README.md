# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim

To identify a real-world sequential decision-making problem and represent it formally as a Markov Decision Process by defining its states, actions, rewards, transitions, and Python representation.

## Problem Statement
A smart phone feature that manages background apps to save battery while keeping the phone fast and smooth throughout the day, even with unpredictable user habits.

## PROBLEM DESCRIPTION
Smartphones need to keep apps running in the background for features like notifications and navigation, but these apps constantly drain the battery and slow down the phone. 
Because everyone uses their phone differently throughout the day, standard background settings either: 
Close apps too aggressively — causing missed alerts and broken background features. 
Allow too much background activity — causing battery drain, lag, and overheating. 
The Challenge: Managing background apps automatically so the phone stays fast and lasts all day, no matter how unpredictable the user's habits are. 

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space
The state space represents here is the discrete battery energy levels of the smartphone, including the terminal condition.



```text
S = {
   Low,
   High,
   Dead,

}
```



---

## Sample State
s = Low



---

## Action Space
The action space consists of the resource management profiles the agent can deploy at any non-terminal decision epoch.

```text
A = {
   Performance mode,
   Saver mode
}
```



## Sample Action

a = Saver mode

## Transition Probability

General form:

$$
P(s' \mid s,a)
$$

This means:

> Probability of reaching next state $s'$ after taking action $a$ in current state $s$.

```
From s = High
𝑃(Low ∣ High,Performance Mode) =0.70
P(High | High,Performance Mode) = 0.30
P(High | High,Saver Mode) = 1.00

From s = Low:
P(Dead | Low, Performance Mode) = 0.90
P(Low | Low, Performance Mode) = 0.10
P(Dead | Low, Saver Mode) = 0.40
P(Low | Low, Saver Mode) = 0.60

From s = Dead (Terminal State):
No actions possible.
 
```


## Reward Function


The reward function defines the feedback received by the agent after taking an action.

General form:

$$
R(s,a,s')
$$


The reward function R(s, a, s') evaluates the utility of the state transition:
Transitioning to any alive state while executing Performance Mode yields a
User Delight reward of +10.

Transitioning to any alive state while executing Saver Mode incurs a Lag 
Penalty reward of -1.

Any transition terminating in the Dead state receives a severe Catastrophe
Penalty reward of -100.


## Graphical Representation

<img width="1082" height="443" alt="image" src="https://github.com/user-attachments/assets/a27671f5-8163-4c45-97d0-0026282f953c" />



## Python Representation
### NAME: NAKUL R 
### REGISTER NUMBER : 212223240102


```python

battery_mdp = {
    'states': ['High', 'Low', 'Dead'],
    'actions': ['Performance Mode', 'Saver Mode'],
    'transitions': {
        'High': {
            'Performance Mode': [
                {'next_state': 'Low', 'probability': 0.70, 'reward': 10},
                {'next_state': 'High', 'probability': 0.30, 'reward': 10}
            ],
            'Saver Mode': [
                {'next_state': 'High', 'probability': 1.00, 'reward': -1}
            ]
        },
        'Low': {
            'Performance Mode': [
                {'next_state': 'Dead', 'probability': 0.90, 'reward': -100},
                {'next_state': 'Low', 'probability': 0.10, 'reward': 10}
            ],
            'Saver Mode': [
                {'next_state': 'Dead', 'probability': 0.40, 'reward': -100},
                {'next_state': 'Low', 'probability': 0.60, 'reward': -1}
            ]
        },
        'Dead': {}
    },
    'discount_factor': 0.90
}


print("--- MDP STATE SPACE ---")
print(f"S = {battery_mdp['states']}\n")

print("--- MDP ACTION SPACE ---")
print(f"A = {battery_mdp['actions']}\n")

print("--- MDP TRANSITIONS & REWARDS LOG ---")
for state, actions in battery_mdp['transitions'].items():
    print(f"Current State: {state}")
    if not actions:
        print("  (Terminal State - No valid actions)")
    for action, outcomes in actions.items():
        print(f"  Action Selected: {action}")
        for outcome in outcomes:
            print(f"    -> Moves to '{outcome['next_state']}' with Probability {outcome['probability']:.2f} | Reward Received: {outcome['reward']}")
print(f"\nDiscount Factor (gamma): {battery_mdp['discount_factor']}")

```

## Output

<img width="592" height="395" alt="image" src="https://github.com/user-attachments/assets/ac907442-63de-469a-b99a-615b9b401bd1" />

## Result


The real-world problem of smartphone battery management was successfully identified and formally mapped to a Markov Decision Process.

