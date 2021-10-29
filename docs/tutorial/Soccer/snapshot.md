# **Game States Snapshot**

In this seciton, you will take snapshots of the game states in your game to support running the game in the `Prediction&Rollback` mode.

## **What Should Be Included in The Snapshot?**

All the game states that affect the game logic simulation result should be included in the snapshot. Let's look at the components in your game logic one by one to identify the states that should be add to the snapshot.

- **External Game States**: The rigidbodies physics states like position, rotation, linear velocity, angular velocity affects the simulation result. They should be included in the snapshot. You will use the FPhysics API to export the physics states.

- **FrameSyncBehaviour States**:
    - `SoccerVehicleController`: The vehicle physics states are stored in the physics engine. The component itself is stateless.
    - `SoccerGoal`: The trigger states: enter, stay, exit is stored in the physics engine. The component itself is stateless.
    - `SoccerGameFlow`: The component is stateful. We should include the player scores, and the timer Id in the snapshot.