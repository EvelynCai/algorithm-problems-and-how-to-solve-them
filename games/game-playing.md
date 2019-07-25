---
description: Summary
---

# Game Playing

### Common Sense

#### 1. Combinatorial Games

**1.1 Definition:** relating to the selection of a given number of elements from a larger number without regard to their arrangements

**1.2 Features:**

* 2 players &lt;- alternate moving
* finite set of portions &lt;- rules specify which positions each player can move to 
* ends when a player can't make a move _\(ref to 2. Winning Strategy\)_

**1.3 Categories:**

1.3.1 impartial games: NIM

1.3.2 partisan games: chess, GO

#### 2. Winning Strategy

**Zermelo’s theorem in game theory**: named after Ernst Zermelo, says that in any finite two-person game of perfect information in which the players move alternatingly and in which chance does not affect the decision making process, if the game cannot end in a draw, then one of the two players must have a winning strategy \(i.e. force a win\)

**2.1 Normal Play:** The player who makes the last move wins. e.g. most impartial games

**2.2 Misere Play:** The player who forces his opponent to make the last move wins, i.e. the player who makes the last move loses. e.g. Nim

#### 3. Game Positions

**3.1 P-position:**  previous player wins, i.e. the player who just made a move wins

**3.2 N-position:** next player wins, i.e. the player who will make a move wins

**3.3 terminal position**: the game state when it ends

**3.4 backwards induction**: terminal position &lt;- P or N?

### Classical Problems

* Leetcode 292 Nim Game
* Leetcode 464 Can I Win
  * with repetition
  * without repetition

