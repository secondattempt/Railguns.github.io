## Paul's blogpost

### Summary

In this blogpost I will do my best to summarise what I have personally worked on throughout the project. My main contribution to the project consists of 2 main classes: TrainSegment and TrackGenerator. The former is responsible with Utilising Unreal's Spline technology to simulate a realistic train carriage or engine, as well its movement and interaction with other segments. The latter is responsible with the procedural generation of the in-game environment. Additionally, I have also worked within the Conductor to implement the train controls, as well as several other features.

### TrainSegment

Inheriting from the AActor class, Unreal's base class for most objects appearing in a world space, the TrainSegment's purpose is to mimick the behaviour of a real world train segment. The first challenge encountered in creating this class was the movement. As such, I was presented with several question:

* How do I create the tracks?
* How do I implement track following mechanics?
* How do I implement track switching?
* How do I implement train segment attachment to each other?
And, later on in the project
* How do I implement two separate train matching their speeds?

#### Tracks and track following

Upon researching my options, I decided that the best course of action was to make use of Unreal's Splines in order to create sets of individual tracks that can be placed together to form complex railways. Due to the lack of C++ documentation and tutorials on the matter, setting up the tracks took more time than I initially anticipated. The method I settled can be brought down to: breaking down the spline (track) into an array of points, each point containing a transform component (position) and rotation, which are used to give each Train segment the corresponding position and rotation that matches the tracks'. The variable speed of the train is, in other words, the variable size of the spline's array iterator.

#### Track switching

Using player input, the lead train segment can be given a custom "orientation" ranging between -1 (left) and 1 (right) which dictates what track it will follow upon encountering a track switch. Extra care was taken to implement a "failsafe" system that makes sure that regardless of the orientation, the closest track will be followed (i.e. if the player is trying to go left, but only a middle track is present, then the train will follow the middle track).

#### Composing a train

Train segments are working well on their own, but our game is about trains, not individual parts of trains. Therefore, I was faced with the challenge of creating a system that enables train segments to follow one another, as if being "attached" to one another. The method I came up allows for plenty of flexibility in terms of train sizes and lengths: if a train segment's "TrainSegmentAtFront" variables is another train segment, it will automatically follow the same track segment, at a customisable distance behind. In case the first train segment switches the track it is on, the train segment following it will wait until it too has reached the end of the curent track, then switch to the segment the train in front of it is following. One possible limitation of this system is that if a track segment is shorter than the train segment itself, it will likely skip over the entire track segment when switching tracks. However, for the purpose of this game, said limitation is practically impossible to encounter.

#### Enemy trains matching speeds

In order to have feasible combat within the game, the enemy trains would have to match the speed of the player train, or wait for it to get within range of combat. This problem was solved by using an adapted version of the train attachment algorithm I previously described. In other words, the enemy train maintains a rederence to the lead player train segment through the "TrainToSyncTo" variable. If the variable is not a null pointer, the train will halve its speed until the train it has to sync to is within a given range. This can be figured out by calculating the distance betweeen the 2 train segments's transforms.

### TrackGenerator

Inheriting from USceneComponent, the TrackGenerator is a class tasked with maintaining the cohesion of the game world by continuously generating tracks for the player train to run on. The concept was to use procedural content generation to create seemingly-random environments, varying from: Free roam-styled tracks, which allow the player to explore at their own leisure, Combat tracks, in which the player is required to fight off an enemy train and, finally, station tracks, which are supposed to act as checkpoints. Given all these features, I broke down the problem into several, smaller, parts, that could be tackled in an Agile fashion by focusing on a single one during each of our sprints:

* How do I attach the tracks together?
* What approach do I take to the track placement algorithm?
* How do I correctly rotate the tracks and match their positions correctly?
* How do I create the environments?
* How do I implement the combat tracks e.g. the secondary track for the enemy train?
* How do I implement the station tracks?
