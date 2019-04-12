# Byron Crowhurst - Contribution to Rail Guns
## Rail Guns Weapon System.

For our game, Rail Guns, I was responsible for the implementation the battle system.

The weapons were meshes that sockets were attached to. A line trace ran from the sockets to a specified range which could be set in editor.
When the line trace hit an object it would return its type as a hit value. This value would be checked and, if the value was equal to that of a train segment, a timer would start. This timer would take the weapons "" as the amount of time to check and then a "deal damage" function would be run from the train segment which took the weapons "damagePerRound" value and subtracted it from the train segments health.

Once the line trace returned a result it was important to then check if the train segment was still in range. This was achieved by disabling the first line trace and running a new one to the previous hit vector. Once this is done a distance check would be done between the hit vector and the weapon and this would determine how to proceed.
If the weapon was in range of the train segment the timer would continue and deal damage would run however if they were no longer in range then the weapon would stop the timer running and return to the original line trace, getting the next train segment to attack.

This method, while appearing simple, was rather complex to achieve correctly and there were many pitfalls to be aware of. These pitfalls informed the design of the weapon class and the way it connected with other classes.
Firstly the weapon needed a reference to the train segment, as it needed to be able to check if it was hitting a train segment and if so which one.
Secondly the train segment needed to know which weapons were attached to it.
This would, regularly, create a circular dependancy however we were able to avoid this problem with the conductor class.
The conductor was responsible for handling the trains connectivity with the rest of the game. This meant including the weapons and the train segments in the conductor class did not create a circular dependancy.

![UML of Weapon](/Pictures/Byron/WeaponClassDiagram.png)

In Unreal a conducter was spawned and then the train segments were spawned and parented to the conductor. Similarly the weapons were spawned in engine and then parented to the train segments. This meant that the weapons were attached to the train segments and rode alongside them.

Some consideration was given to how a player would select the train segments and have the weapons fire at other train segments but due to time constraints this did not manage to make it into the game, though some remnents from our efforts can be seen.
