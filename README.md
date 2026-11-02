# Representation of a Real-World Problem as a Markov Decision Process

## Aim

To represent a real-world problem as a Markov Decision Process (MDP) by identifying its states, actions, transition probabilities, and reward function.

## Problem Statement

An AI-based car navigation system is designed to guide a car from its starting location to a desired destination. The system observes the current road condition and decides whether to move forward, turn, or wait based on traffic conditions.

The objective is to reach the destination efficiently while minimizing travel time, traffic delays, and unnecessary movements.

## Problem Description

The AI car navigation system operates using five states representing different road locations and conditions. At each state, the AI chooses one of three actions:

- Move Forward
- Turn
- Wait

The system receives positive rewards for reaching the destination and making progress toward the goal. It receives penalties for traffic delays and unnecessary waiting.

The problem can be represented using a Markov Decision Process:

**MDP = (S, A, P, R, γ)**

Where:

- **S** = Set of states
- **A** = Set of actions
- **P** = Transition probability
- **R** = Reward function
- **γ** = Discount factor

## MDP Components

| Component | Description |
|---|---|
| Agent | AI Car Navigation System |
| Environment | Roads, junctions, and traffic conditions |
| States | Five road locations or conditions |
| Actions | Move Forward, Turn, Wait |
| Transition Probability | Probability of reaching the next state |
| Reward | Feedback based on travel progress and delays |
| Goal | Reach the destination efficiently |
| Discount Factor | γ = 0.9 |

## State Space

The state space represents the possible locations or road conditions encountered by the car.

**S = {S1, S2, S3, S4, S5}**

The five states are:

- **S1 – Starting Point:** The initial location of the car.
- **S2 – Clear Road:** A road with light traffic.
- **S3 – Traffic Junction:** An intersection where the car may need to turn.
- **S4 – Heavy Traffic:** A road with congestion and delays.
- **S5 – Destination:** The final location.

## Sample State

Suppose the car is currently travelling on a clear road.

**s = S2 (Clear Road)**

The AI system must choose an action that moves the car closer to its destination.

## Action Space

The action space represents the possible decisions taken by the AI car navigation system.

**A = {Move Forward, Turn, Wait}**

The actions are:

1. **Move Forward:** Continue along the current road.
2. **Turn:** Change direction at a junction.
3. **Wait:** Pause temporarily to allow traffic to clear.

## Sample Action

Suppose the car is at S2 (Clear Road) and needs to reach S5 (Destination). The AI selects:

**a = Move Forward**

The car moves toward the traffic junction.

**S2 → Move Forward → S3**

## Transition Probability

The transition probability represents the probability of reaching a new state after taking an action.

General form:

**P(s′ | s, a)**

This means the probability of reaching the next state s′ after taking action a in the current state s.

For this experiment, transitions are simplified and stochastic to represent uncertainty in road and traffic conditions.

### Transition Probability Table

| Current State | Action | Next State | Probability |
|---|---|---|---:|
| S1 – Starting Point | Move Forward | S2 – Clear Road | 0.9 |
| S1 – Starting Point | Move Forward | S4 – Heavy Traffic | 0.1 |
| S2 – Clear Road | Move Forward | S3 – Traffic Junction | 0.8 |
| S2 – Clear Road | Move Forward | S4 – Heavy Traffic | 0.2 |
| S3 – Traffic Junction | Turn | S5 – Destination | 0.7 |
| S3 – Traffic Junction | Turn | S4 – Heavy Traffic | 0.3 |
| S4 – Heavy Traffic | Wait | S2 – Clear Road | 0.6 |
| S4 – Heavy Traffic | Wait | S4 – Heavy Traffic | 0.4 |
| S5 – Destination | Stop | S5 – Destination | 1.0 |

The transition probabilities for each listed state-action pair sum to 1.0. This table shows selected transitions for the simplified model rather than every possible state-action combination.

### Example Transition

**P(S3 | S2, Move Forward) = 0.8**

This means that when the car is on a clear road and chooses to move forward, there is an 80% probability of reaching the traffic junction.

## Reward Function

The reward function defines the feedback received by the AI agent after taking an action.

General form:

**R(s, a, s′)**

The reward system is defined as follows:

| Situation | Reward |
|---|---:|
| Reaches the destination | +10 |
| Moves closer to the destination | +5 |
| Traffic clears after waiting | +2 |
| Encounters heavy traffic | -3 |
| Unnecessary waiting or movement | -2 |

A positive reward encourages the car to reach its destination efficiently. Negative rewards discourage delays and unnecessary actions.

The discount factor is:

**γ = 0.9**

The discount factor determines the importance of future rewards compared with immediate rewards.

### Sample Reward

Suppose the car is at S3 (Traffic Junction). The AI selects Turn, and the car reaches S5 (Destination).

**S3 → Turn → S5**

The car successfully reaches its destination and receives a reward of **+10**.

## Graphical Representation

The MDP graph represents the five states as nodes and the actions as directed transitions.

The graph includes:
1. States as nodes.
2. Actions as arrows.
3. Transition probabilities on the arrows.
4. Rewards associated with transitions.

### Sample Transition Diagram

- S1 (Starting Point) → S2 (Clear Road)
- S1 (Starting Point) → S4 (Heavy Traffic)
- S2 (Clear Road) → S3 (Traffic Junction)
- S2 (Clear Road) → S4 (Heavy Traffic)
- S3 (Traffic Junction) → S5 (Destination)
- S3 (Traffic Junction) → S4 (Heavy Traffic)
- S4 (Heavy Traffic) → S2 (Clear Road)
- S4 (Heavy Traffic) → S4 (Heavy Traffic)
- S5 (Destination) → S5 (Destination)

Example transition:

**S3 — Turn / P = 0.7 / Reward = +10 → S5**

This means that when the car turns at the traffic junction, it has a 70% probability of reaching the destination and receives a positive reward for successful arrival.

## Python Representation

```python

# States
states = {
    0: "Starting_Point",
    1: "Clear_Road",
    2: "Traffic_Junction",
    3: "Heavy_Traffic",
    4: "Destination"
}

# Actions
actions = {
    0: "Move_Forward",
    1: "Turn",
    2: "Wait",
    3: "Stop"
}

# MDP Transition Definition
P = {
    0: {
        0: [(0.9, 1, 5.0, False), (0.1, 3, -3.0, False)],
        1: [(1.0, 0, -2.0, False)],
        2: [(1.0, 0, -2.0, False)],
        3: [(1.0, 0, -2.0, False)]
    },
    1: {
        0: [(0.8, 2, 5.0, False), (0.2, 3, -3.0, False)],
        1: [(1.0, 2, 5.0, False)],
        2: [(1.0, 1, -2.0, False)],
        3: [(1.0, 1, -2.0, False)]
    },
    2: {
        0: [(1.0, 3, -3.0, False)],
        1: [(0.7, 4, 10.0, True), (0.3, 3, -3.0, False)],
        2: [(1.0, 2, -2.0, False)],
        3: [(1.0, 2, -2.0, False)]
    },
    3: {
        0: [(1.0, 3, -3.0, False)],
        1: [(1.0, 3, -2.0, False)],
        2: [(0.6, 1, 2.0, False), (0.4, 3, -2.0, False)],
        3: [(1.0, 3, -2.0, False)]
    },
    4: {
        0: [(1.0, 4, 0.0, True)],
        1: [(1.0, 4, 0.0, True)],
        2: [(1.0, 4, 0.0, True)],
        3: [(1.0, 4, 0.0, True)]
    }
}

# Discount Factor
gamma = 0.9

# Display MDP Definition
print("States:")
print(states)

print("\nActions:")
print(actions)

print("\nMDP Transition Definition:")
print(P)

print("\nDiscount Factor (gamma):")
print(gamma)

```

## Output

```text
States:
{0: 'Starting_Point',
 1: 'Clear_Road',
 2: 'Traffic_Junction',
 3: 'Heavy_Traffic',
 4: 'Destination'}

Actions:
{0: 'Move_Forward',
 1: 'Turn',
 2: 'Wait',
 3: 'Stop'}

MDP Transition Definition:
{
  0: {
    0: [(0.9, 1, 5.0, False), (0.1, 3, -3.0, False)],
    1: [(1.0, 0, -2.0, False)],
    2: [(1.0, 0, -2.0, False)],
    3: [(1.0, 0, -2.0, False)]
  },
  1: {
    0: [(0.8, 2, 5.0, False), (0.2, 3, -3.0, False)],
    1: [(1.0, 2, 5.0, False)],
    2: [(1.0, 1, -2.0, False)],
    3: [(1.0, 1, -2.0, False)]
  },
  2: {
    0: [(1.0, 3, -3.0, False)],
    1: [(0.7, 4, 10.0, True), (0.3, 3, -3.0, False)],
    2: [(1.0, 2, -2.0, False)],
    3: [(1.0, 2, -2.0, False)]
  },
  3: {
    0: [(1.0, 3, -3.0, False)],
    1: [(1.0, 3, -2.0, False)],
    2: [(0.6, 1, 2.0, False), (0.4, 3, -2.0, False)],
    3: [(1.0, 3, -2.0, False)]
  },
  4: {
    0: [(1.0, 4, 0.0, True)],
    1: [(1.0, 4, 0.0, True)],
    2: [(1.0, 4, 0.0, True)],
    3: [(1.0, 4, 0.0, True)]
  }
}

Discount Factor (gamma):
0.9
```

## Result

The real-world AI car navigation problem was successfully represented as a Markov Decision Process. Five states, four possible actions, transition probabilities, a reward function, and a discount factor were defined and implemented using Python.

This MDP demonstrates how an AI navigation system can make decisions based on road conditions to reach a destination while minimizing traffic delays and unnecessary movements.
