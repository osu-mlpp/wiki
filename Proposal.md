# MLpp (Machine Learning performance points) system proposal
## project goals / general idea

**TODO**: Evaluate part.

In this project, we aim to create a good pp algorythm with the use of statistics and machine learning.  
Statistics on player scores on beatmaps (and on beatmaps patterns from player replays) will be used to generate the training and testing sets to train a neural network that takes a beatmap data (or some pattern specific data) as input (with some preprocessing, but no statistics) and outputs data that allows us to have a good estimate of the pp values of scores.

## Notes about v2, modes and mods

**TODO**: Evaluate part.

#### Score v2 and slider accuracy

In score v2 (and in osu!lazer), sliders have to be timed accurately like normal hitcircles, while in score v1 (the currently used system), you'll do a 300 even if you are in the timing window of 100s or 50s (but you'll still miss or slider break if it's outside of the 50s range). This aspect shouldn't particularly affect the proposal, as accuracy will at least be considered for normal hitcircles anyway, and we'll consider that we are still in score v1 for now as we don't have much score v2 data yet and it will allows us to compare the results with the current system pp values, even if the MLpp system would ultimately have to be made for score v2.

#### Gamemodes

Please note that this document is written with the main osu! gamemode in mind (which is osu! standard) but should be easily adaptable to other gamemodes in the future. A part about adapting MLpp to other modes will be added in the future if judged necessary.

#### Mods

Since mods in osu! completely change the difficulty of a beatmap, to simplify the writting and reduce redondant formulations in this document, a beatmap will (most of the time) refer to a single difficulty of a beatmapset with some combination of mods (nomod being one combination). This means that the same beatmap with different combinations of mods will be considered as different beatmaps unless precised otherwise.

## Note about values considered in scores (only max-combo, acc and miss-counts ?)

**TODO** (high prio)

## Link to details

...