## Goal
The goal of this project is to try to define a more accurate way to evaluate a score's pp value on a map using existing map statistics and machine learning.

## General idea
### Part 1 - Probability and Theory
#### Step 1 - The function P
We first define the following function :  
<img src="https://render.githubusercontent.com/render/math?math=P(b,s,l) =\text{Probability that a random player of skill level l can do a score s or better on beatmap b}">

where :
- `b` represents a beatmap (which we will often refer as map) with a defined gamemode and set of mods. (But we will first focus on osu! std gamemode)
- `s` represents a score defined as a tuple of this kind : `(max_combo, miss_count, accuracy, etc...)` (The list of values considered need to be defined)
- doing s or better means doing any score that is equal or better in every aspects (equal or higher max_combo AND equal or lower miss_count AND etc...)
- `l` represents an estimation of the "player skill" (as a single scalar)

#### Step 2 - The curve f
For a beatmap b and a score s we can then define the function :  
<img src="https://render.githubusercontent.com/render/math?math=f_{(b,s)}(l) = P(b,s,l)">
- This function maps the level estimation domain (for example [0,+inf] if we use ppv2 as level estimation) to the probability range [0,1].
- This function is assumed to be monotonically increasing since an increase of the skill estimate is correlated with and increase of actual skill which itself is correlated with an increase in probability of doing a better score.
- We assume that for maps and scores that are sufficiently "doable", for any value `t` in `(0,1)`, there is a value `λ` such that  
<img src="https://render.githubusercontent.com/render/math?math=\forall l, l \gt \lambda \iff f_{(b,s)}(l) = P(b,s,l) \gt t">

#### Step 3 - Defining a new pp value from f
Note that the weighted average (using the same top-play weights as ppv2) pp value of the maps considered in a player's pp calculation is approximately 1/20th of the player pp value.  
From that, if we have `P` we can re-estimate the pp values of previous scores :
- Choose a threshold `t` (a good threshold is probably arround 5 to 10%, we'll have to find out)
- Find the value `λ` which satisfies the equation above
- redefine the pp value of the score as `λ/20`

#### Step 4 - Convergence of the system
We claim that, if the threshold `p` is well chosen, this new pp value should be a better estimation that the level estimation metric used as input for l.
To analyse that, let's compare two curves `f(l)=P(b1,s1,l)` and `g(l)=P(b2,s2,l)` for two pairs of beatmaps and score `x1 = (b1,s1)` and `x2 = (b2,s2)` :
- if `x1` is harder to achieve than `x2` for players of level `l`, then `f(l) < g(l)` (the probability that a player of level `l` achieves `x1` is lower than the probability that he achieves `x2`).
- From that point, if two `x1` and `x2` that are estimated as having the same value in the input skill estimation system, if `x1` is more underweighted that `x2`, this means that `x1` is harder than `x2` for at least some players of skill level `l`, which means that we will have `f(l) < g(l)` in some part of the curve.
- Following that, if the threshold `t` is well chosen, the score `x1` will be given a lower pp value than `x2` using the method above.

#### Conclusion
While applying this system does not give a perfect system, this should give a better system that the one used as input for the estimation of the level of the players.
This also means that we can apply this system iteratively to converge progressely to an "ideal" system, and progressively get away from the bias induced by the original input system.
The difficult tasks that remains are finding a good estimation the function `P`, and choosing a good threshold `t`

### Part 2 : Estimating P from statistics
TODO

### Part 3 : Estimating P using Machine Learning
TODO