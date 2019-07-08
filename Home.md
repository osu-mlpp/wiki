# MLpp Project wiki

Welcome to the osu! MLpp project wiki!

**WARNING:** This wiki (and project) is a **Work in Progress** !

## Table of content

Here is the (planned) table of content of the Wiki :

- Introduction to osu! and osu! keywords (low prio)
    - osu! presentation (for non-players)
    - Dictionary (for non-players and casuals)
        - osu! general keywords (Modes, mods, beatmaps/maps, mapsets, ...)
        - osu! scores (SS/S/A/B/C, FC, acc, combo, miss/sb/100/50, v2, ...)
        - osu! beatmap objects (hitobjects, hitcircle, slider, spinner, ...)
        - osu! beatmap values ()
        - osu! mods (HD, HR, DT, EZ, FL, ...)
        - ... ?
- Introduction to previous pp systems and project motivation (mid prio)
    - pp system definition
    - rought presentation of pp v1
    - pp v1 problems
    - rought presentation of pp v2
    - pp v2 problems
    - general advantages and problems of statistical method
    - how Machine Learning can help
- Introduction to mathematical and technical definitions
    - Maths definitions...
    - definition of skill
    - ... ?
- MLpp (Machine Learning performance points) system proposal
    - project goals / general idea (highest prio)
    - Note about v2, modes and mods (high prio)
    - Note about values considered in scores (only max-combo, acc and miss-counts ?) (high prio)
    - Part 1 : PP from Statistics (highest prio)
        - stat #1 : Map appearance in players top 100 and correlation with their pp.
            - Definition
            - Limited usage : Detect over/under-rated map & rate system balance
        - stat #2 : % of players of skill X with scores above Y
            - Definition
            - Current pp as approximation of skill
            - pp estimation from stats
            - Advantages
            - Outliers/Nuissance and countermeasures
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
        - Conclusions (Resumee of how we will proceed)
    - Part 2 : Neural Network (mid prio)
        - Network output (Multiple choices)
        - Network input (Multiple choices)
        - Network shape and structure (Multiple choices)
        - From patterns back to whole map pp
            - ... ?
        - Sliting the work
            - Acc/Aim/Speed/? neural networks
    - Part 3 : MLpp in production (low prio)
        - ppv2 + mlpp mix ?
        - Live trainability
        - ...
- Required Data for the project / Request to peppy (high prio)
- Roadmap and Schedule (high prio)
- ... ?


## Introduction to osu! and osu! keywords

**TODO** (low prio)

## Introduction to previous pp systems and project motivation

**TODO** (mid prio)

## Introduction to mathematical and technical definitions

**TODO** (while writting)

## MLpp (Machine Learning performance points) system proposal
### project goals / general idea

**TODO** (highest prio)

### Note about v2, modes and mods

**TODO** (high prio)

### Note about values considered in scores (only max-combo, acc and miss-counts ?)

**TODO** (high prio)

### Part 1 : PP from Statistics

**TODO** (highest prio)

### Part 2 : Neural Network

**TODO** (mid prio)

### Part 3 : MLpp in production

**TODO** (low prio)

## Required Data for the project / Request to peppy

**TODO** (high prio)

## Roadmap and Schedule

**TODO** (high prio)
