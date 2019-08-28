# MLpp (Machine Learning performance points) system proposal
## project goals / general idea

**TODO**: Evaluate part.

In this project, we aim to create a good pp algorithm with the use of statistics and machine learning.  
Statistics on player scores on beatmaps (and on beatmaps patterns from player replays) will be used to generate the training and testing sets to train a neural network that takes a beatmap data (or some pattern specific data) as input (with some preprocessing, but no statistics) and outputs data that allows us to have a good estimate of the pp values of scores.

## Notes about v2, modes and mods

**TODO**: Evaluate part.

#### Gamemodes

Please note that this document is written with the main osu! gamemode in mind (which is osu! standard) but should be easily adaptable to other gamemodes in the future. A part about adapting MLpp to other modes will be added in the future if judged necessary.

#### Mods

Since mods in osu! completely change the difficulty of a beatmap, to simplify the writing and reduce redundant formulations in this document, a beatmap will (most of the time) refer to a single difficulty of a beatmapset with some combination of mods (nomod being one combination). This means that the same beatmap with different combinations of mods will be considered as different beatmaps unless precised otherwise.

#### Score v2 and slider accuracy

In score v2 (and in osu!lazer), sliders have to be timed accurately like normal hitcircles, while in score v1 (the currently used system), you'll do a 300 even if you are in the timing window of 100s or 50s (but you'll still miss or slider break if it's outside of the 50s range). This aspect shouldn't particularly affect the proposal, as accuracy will at least be considered for normal hitcircles anyway, and we'll consider that we are still in score v1 for now as we don't have much score v2 data yet and it will allow us to compare the results with the current system pp values, even if the MLpp system would ultimately have to be made for score v2.

## Note about values considered in scores (only max-combo, acc and miss-counts ?)

**TODO**: Evaluate part. Define "ranking panel" ?

As of today, in ppv2, only the max-combo, miss-count and accuracy values of the players score are considered to determine the pp value of the score. While we can do a  better estimation of skill than ppv2 with only those 3 values, we should be able to do even better if we use other meaningful values.

One thing that is completely ignored in ppv2 is the non-max combos. The combo you do in other parts doesn't matter, which means that, outside of the max combo part, misses all have the same impact on pps no matter where they are and slider breaks too, as they have the same impact as hitcircle 100s and only change the accuracy value.

While the pp is not impacted by non-maximum combos, the score is, both in score v1 and score v2, which makes it even more meaningful to use the non-maximum combos in pp calculation.
The scorev1 score is **roughly proportional** to `sum_i(combo_i^2) * accuracy` and I think using the sum of squared combos in the pp value estimation would help to get more accurate values. Unfortunately, the values of non-max combos are not stored in the score database, but it's possible to estimate the value of the sum of squared combos by dividing the total score of the player by its accuracy and the [other factors](https://osu.ppy.sh/help/wiki/Score/#score). The square-root of squared combo is also a good estimate of "average combo" along the map.
It's also possible to use the score itself instead of trying to estimate the sum of the squared combos, as the multiplication by the accuracy is not necessarily unwanted, and the other factors are constants.
We could also consider using a lower power than 2 in the sum, to give more impact to lower combos than they currently have in scorev1.

In the future we might want to add more values into the mix, but I guess we should be fine with what we have for now, and adding much more values would reduce the "arcade" aspect of the game if the values used are not both displayed in the ranking panel and easily understandable by the players.

## Link to details

... 