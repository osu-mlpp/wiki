# MLpp Project wiki - Tablet of content

Welcome to the osu! MLpp project wiki!

**WARNING:** This wiki (and project) is a **Work in Progress** and probably has **outdated information** !
Check out the [Summary](Summary) for the most up-to-date information.

Here is the (planned) table of content of the Wiki :

- [Introduction to osu! and osu! keywords](Intro-osu) (low prio)
    - osu! presentation (for non-players)
    - Dictionary (for non-players and casuals)
        - osu! general keywords (Modes, mods, beatmaps/maps, mapsets, ...)
        - osu! scores (SS/S/A/B/C, FC, acc, combo, miss/sb/100/50, v2, ...)
        - osu! beatmap objects (hitobjects, hitcircle, slider, spinner, ...)
        - osu! beatmap values ()
        - osu! mods (HD, HR, DT, EZ, FL, ...)
        - ... ?
- [Introduction to previous pp systems and project motivation](Intro-pp) (mid prio)
    - pp system definition
    - quality of a pp system
    - rough presentation of pp v1
    - pp v1 problems
    - rough presentation of pp v2
    - pp v2 problems
    - general advantages and problems of statistical method
    - how Machine Learning can help
- [Introduction to mathematical and technical definitions](Intro-tech)
    - Math definitions...
    - definition of skill
    - ... ?
- [MLpp (Machine Learning performance points) system proposal](Proposal)
    - project goals / general idea (highest prio)
    - Notes about v2, modes and mods (high prio)
    - Note about values considered in scores (only max-combo, acc and miss-counts ?) (high prio)
    - [Part 1 : PP from Statistics](Part1-stats) (highest prio)
        - stat #1 : Map appearance in players top 100 and correlation with their pp.
            - Definition
            - Limited usage : Detect over/under-rated map & rate system balance
        - stat #2 : % of players of skill X with scores above Y
            - Definition
            - Current pp as approximation of skill
            - pp estimation from stats
            - Advantages
            - Outliers/Nuisance and countermeasures
                - Why under/over-ranked players don't matter much
                - Players with < 100 top-plays
                - Non-passes and non-finished plays
                - Map play-counts per player
                - Score/Map age
                - Currently frequent patterns
            - Statistical accuracy/uncertainty handling
            - Rank to pp curve shape and potential remodeling
            - Iterations and convergence
            - From whole map to map-patterns
        - Conclusions (Summary of how we will proceed)
    - [Part 2 : Neural Network](Part2-NN) (mid prio)
        - Network output (Multiple choices)
        - Network input (Multiple choices)
        - Network shape and structure (Multiple choices)
        - From patterns back to whole map pp
            - ... ?
        - Splitting the work (simplify training)
            - Acc/Aim/Speed/? neural networks
        - Dataset augmentation (?)
        - ...
    - [Part 3 : MLpp in production](Part3-production) (low prio)
        - ppv2 + mlpp mix ?
        - Live trainability
        - ...
- [Request of required Data](Data-request) (high prio)
- [Roadmap and Schedule](Roadmap) (high prio)
- [Contributors](Contributors)
- [Logs of MLpp contributions](Logs)