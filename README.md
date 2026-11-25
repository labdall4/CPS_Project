# CPS_Project
## Project Overview

### Part 1: Background and Motivation

In Cyber-Physical Systems (CPSs), real-time analysis and optimal strategy selection are essential for many real-world applications. This project explores the intersection of computer vision, game theory, and automated decision-making through the implementation of an AI-assisted system to play the game of Rock-Paper-Scissors-Minus-One (RPS-1).

RPS-1 is an extension of the [intransitive](https://en.wikipedia.org/wiki/Intransitive_game) [hand game](https://en.wikipedia.org/wiki/Hand_game) of [Rock Paper Scissors](https://en.wikipedia.org/wiki/Rock_paper_scissors) (RPS). In the standard RPS game, usually played between two players, each player simultaneously forms one of three shapes with an outstretched hand: **rock** (a closed fist), **paper** (a flat hand), or **scissors** (a fist with the index finger and middle finger extended, forming a *V*).  The term *intransitive* means that the pairwise competitions between the strategies form a cycle.

![Rock-paper-scissors rules showing which hand shape defeats each other shape](https://upload.wikimedia.org/wikipedia/commons/6/67/Rock-paper-scissors.svg)
[image courtesy](https://en.wikipedia.org/wiki/File:Rock-paper-scissors.svg)
In this project, the camera observes physical hand gestures, the software interprets the image and selects a strategy, and a human player carries out the recommended action. This is a human-in-the-loop interaction: the system recommends which hand to retain, but it does not physically move the player's hands.

RPS-1 is a strategic variant where two players simultaneously display two hands each (four hands total), then simultaneously withdraw one hand each, with the winner determined by standard rock-paper-scissors rules applied to the remaining hands. This creates a complex decision space where the objective is to maximize expected payoff against an opponent choosing their own strategy. An optimal mixed strategy does not require knowing the opponent's next action and does not guarantee a win in every round.

In the context of game theory, RPS is a [simultaneous](https://en.wikipedia.org/wiki/Simultaneous_game), [zero-sum](https://en.wikipedia.org/wiki/Zero-sum_game) game. RPS-1 is a two-stage game with simultaneous choices within each stage:

- In a **simultaneous** stage, each player chooses their action without knowing the action the other player is choosing at that stage. In Stage 2 of RPS-1, both players have already seen the hand shapes displayed in Stage 1.
- A [**zero-sum**](https://en.wikipedia.org/wiki/Zero-sum_game) game is a game in which an advantage for one side corresponds to an equivalent loss for the other. Here, the two players' payoffs sum to zero in each round.


***

#### Game Theory

To analyze the optimal strategies, consider the following payoff for each round:
1. 1 point for a win,
1. 0 points for a tie, and
1. -1 point for a loss.

Assume that Player-1 displays **PS** (Paper + Scissors) and Player-2 displays **PR** (Paper + Rock) in Stage 1. The **payoff** matrix for Player-1 in Stage 2 is shown below. Rows represent the shape Player-1 retains, and columns represent the shape Player-2 retains:

|  | Paper | Rock  |
| ----- | ----- | ----- |
| Paper | 0 | 1  |
| Scissors | 1 | -1 |

You may infer that, *if the objective of the game is **not to lose**, then Player-1 should always play paper*, as it ties against paper and wins against rock, so it never loses. However, **is this the best payoff**?

The objective in this project is to maximize expected payoff, using the scores above. This differs from maximizing win probability alone because losses also contribute to the payoff. For the equilibrium strategy, consider an opponent who also chooses a strategy optimally.
