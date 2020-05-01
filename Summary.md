## Goal
The goal of this project is to try to define a more accurate way to evaluate a score's pp value on a map using existing map statistics and machine learning.

## General idea
### 1 - Probability and Theory
#### 1.1 - The function P
We first define the following function :

<img src="https://render.githubusercontent.com/render/math?math=\large P(b,s,l) =\text{Probability that a random player of skill level l can do better that a score s on beatmap b}">

where :
- `b` represents a beatmap (which we will often simply refer as map) with a defined gamemode and set of mods. (But we will first focus on osu! std gamemode)
- `s` represents a score defined as a tuple of this kind : `(max_combo, miss_count, accuracy, etc...)` (The list of values considered need to be defined)
- "better" means doing any score that is equal or better in every aspects (equal or higher max_combo AND equal or lower miss_count AND etc...)
- `l` represents an estimation of the "player skill" (as a single scalar)

Also, in the future, a map (`b`) will almost always include the information of the set of mods (and of course the gamemode) it is being played with, unless it is precised otherwise.  
In the same way, we will often refer the tuple `x = (b,s)` as "score", since a score has no meaning without the map it was made on.  
To simplify the writing even more, we say that `x` and the tuple `(b,s)` are interchangeable, which gives for example : `P(x,l) = P(b,s,l)`.  
When we are talking of a score, it should be clear from the context whether it is a universal score (`s`) or a beatmap-specific score (`x`) but we will otherwise specify.

#### 1.2 - The curve f
For a score x we can then define the function :

<img src="https://render.githubusercontent.com/render/math?math=\large f_{(b,s)}(l) = f_x(l) = P(x,l)">

- This function maps the level estimation domain (for example [0,+∞] if we use ppv2 as level estimation) to the probability range [0,1].
- This function is assumed to be monotonically increasing since an increase of the skill estimate is correlated with and increase of actual skill which itself is correlated with an increase in probability of doing a better score.

We then assume that for maps and scores that are sufficiently "doable", for any value `t` in `(0,1)`, there is a value `λ` such that :

<img src="https://render.githubusercontent.com/render/math?math=\large \forall l, l \gt \lambda \iff f_x(l) = P(x,l) \gt t">

Note : <img src="https://render.githubusercontent.com/render/math?math=\iff"> means "if and only if" or "is equivalent to". This means that there is a value `λ` such that if <img src="https://render.githubusercontent.com/render/math?math=l \gt \lambda"> then <img src="https://render.githubusercontent.com/render/math?math=P(x,l) \gt t"> and vice-versa.

#### 1.3 - Defining a new pp value from f
Note that the weighted average (using the same top-play weights as ppv2) pp value of the maps considered in a player's pp calculation is approximately 1/20th of the player pp value.  
From that, if we have `P` we can re-estimate the pp values of previous scores :
- Choose a threshold `t` (a good threshold is probably arround 5 to 10%, we'll have to find out)
- Find the value `λ` which satisfies the equation above
- redefine the pp value of the score as `λ/20`

It is also possible to define `λ` in other ways than from a simple threshold `t` that could achieve better results and we will explore those other possibilities, but the idea will remain similar.

#### 1.4 - Convergence of the system
We claim that, if the threshold `t` is well chosen, this new pp value should be a better estimation that the level estimation metric used as input for l.
To analyse that, let's compare two curves `f(l)=P(x1,l)` and `g(l)=P(x2,l)` for two scores `x1 = (b1,s1)` and `x2 = (b2,s2)` :
- if `x1` is harder to achieve than `x2` for players of level `l`, then `f(l) < g(l)` (the probability that a player of level `l` achieves `x1` is lower than the probability that he achieves `x2`).
- From that point, if two `x1` and `x2` that are estimated as having the same value in the input skill estimation system (e.g. ppv2), if `x1` is more underweighted that `x2`, this means that `x1` is harder than `x2` for at least some players of skill level `l`, which means that we will have `f(l) < g(l)` in some part of the curve.
- Following that, if the threshold `t` is well chosen, the score `x1` will be given a lower pp value than `x2` using the method above, which guarantees convergence.

#### 1.5 - Conclusion
While applying this system does not give a perfect system, this should give a better system that the one used as input for the estimation of the level of the players.
This also means that we can apply this system iteratively to converge progressely to an "ideal" system, and progressively get away from the bias induced by the original input system.
The difficult tasks that remains are finding a good estimation the function `P`, and choosing a good threshold `t`

### 2 - Estimating P from statistics
Since P is a probabily, it is natural to try to estimate it from statistics.

#### 2.1 - Sampling
For some score `x = (b,s)`, we can try to estimate the curve `f(l)=P(x,l)` in the following way :
We define sampling points `L_i` with `i` in `{1,2,...,n}` at which we will try to estimate `f(L_i)`.
To do so, the easiest way is to take `S` the set of all scores on beatmap b done by players of level `l` in `[L_i-r,L_i+r]` for some small positive value `r` and estimate `f(L_i)` as the percentage of scores in `S` that are better than `s`, with "better" as defined previously.
A simple choice for the sampling points `L_i` can be `100*i` if L is defined in with ppv2, and then defining `r = 50` seems a natural choice to cover the whole spectrum of players.
An other way to sample can be to give scores a weight depending on player's level distance to the sampling point `|L_i - l|`.
It is also possible to define the sampling points from other metrics like play time but ppv2 seems to be the best skill estimation available as of now, and a better input level estimation means a faster convergence.
It is also possible to use the ppv2 rank instead, or any monotone function of the rank, like `h(rank) = log(active_player_count)-log(rank)` (We will explore this possibility later), as it keeps the ordering of ppv2 while allowing us to choose what we want the final pp to rank curve to look like.

Once we have the estimation of the values of `f(L_i)` for all `L_i`, we can then interpolate to estimate the value of `f(l)` for any `l`, and estimate the pp value of the score by applying the method defined in 1.3.

#### 2.2 : Biases
The statistic above is subject to many biases and other aspect of difficulty that we ignored till then. We will need to identify them, estimate their impact on the results, and eventually apply corrections.
Examples of such biases are :
- Players where pp provides a very bad skill estimation (new players with low amount of scores, derankers)
- Players not willing to finish the map even while he could clear it
- Different kinds of players playing different kinds of maps
- The amount of retries of a player on the map
- Variance in rarity of patterns in currently available beatmaps (partially due to pp mapping), and it's effects on how trained the player are on those patterns
- Distribution of ages of scores (which is correlated with the age of the beatmap)

#### 2.3 - Lack of data
While these statistics should allow to estimate the pp value of a lot of scores, there will be imprecissions depending on how much scores we have in our samples.
We will try to measure this imprecision in order to be able to know which pp values are meaningfull and which are not.
For some scores, it will be impossible to do any good estimation as we will lack data, especially for the top players that do unique scores.
For that reason, we will need to be able to predict `P` on beatmap/scores that don't have statistics, and this is where we will use Machine learning.

### 3 : Estimating P using Machine Learning

TODO...
