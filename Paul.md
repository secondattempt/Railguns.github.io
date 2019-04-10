## Paul's blogpost

### Summary

In this blogpost I will do my best to summarise what I have personally worked on throughout the project. My main contribution to the project consists of 2 main classes: TrainSegment and TrackGenerator. The former is responsible with Utilising Unreal's Spline technology to simulate a realistic train carriage or engine, as well its movement and interaction with other segments. The latter is responsible with the procedural generation of the in-game environment.

### TrainSegment

Inheriting from the AActor class, Unreal's base class for most objects appearing in a world space, the TrainSegment's purpose is to mimick the behaviour of a real world train segment. The first challenge encountered in creating this class was the movement. As such, I was presented with several question:
* How do I create the tracks?
* How do I implement track following mechanics?
* How do I implement track switching?
* How do I implement train segment attachment to each other?

### TrackGenerator
