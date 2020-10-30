# StaticFrameSyncBehaviour

## FrameSync managed updates
`StaticFrameSyncBehaviour` registers its GameObject to the FrameSyncEngine.

When the `FrameSyncEngine` simulates a frame, it prepares the player inputs for the frame and notifies all the registered `StaticFrameSyncBehaviour`s to update.

When a `StaticFrameSyncBehaviour` got notified about the simulation, it excutes the `FrameSyncUpdate()` method of the `IFrameSyncUpdate` MonoBehaviour components of its GameObject.

???+ info
    You can think of `FrameSyncUpdate()` as the FrameSync version of the Unity `Update()`. It is called every FrameSync frame. Your behaviour and logic should be excuted in the `FrameSyncUpdate()` method. 

## FrameSync managed data

When the `FrameSyncEngine` finished simulating a frame, it notifies all the registered `StaticFrameSyncBehaviour`s to export their data. The exported data is used for the FrameSync consensus mechanism to achieve the agreement on the simulation results among different players across the network.

When a `StaticFrameSyncBehaviour` is asked to export its data, it excutes the `Export()` method of the `IFrameSyncData` MonoBehaviour components of its GameObject.

When a `StaticFrameSyncBehaviour` is asked to restore to a frame, it excutes the `Import()` method of the `IFrameSyncData` MonoBehaviour components of its GameObject with the saved data.

## Which GameObject should have a StaticFrameSyncBehaviour?

You have the following Rigidbodies active in the game. 

Name    | Body Type | Description
--------| --------- | ----------------
Ball    | Dynamic   | Controlled by physics
Paddles | Kinematic | Controlled by players
Walls   | Staic     | Do not move


- For the Paddles, they read player inputs to move and their position information should be exported, so we should add `StaticFrameSyncBehaviour` to them.

- For the Ball, it does boundary check every frame and its position information should be exported, so it should have a `StaticFrameSyncBehaviour`.

- For the Walls, they do not move and their physical data does not change so we do not need to add `StaticFrameSyncBehaviour` to them.

## Adding the StaticFrameSyncBehaviour componennt

- Select the `Ball` and the `Paddle`s in the `Hierarchy` window and add `StaticFrameSyncBehaviour` to them by selecting `Add Component`->`Static Frame Sync Behaviour`.

## Assign the StaticFrameSyncBehaviourID

You need to assign different `StaticFrameSyncBehaviourID` to the `StaticFrameSyncBehaviour` in your scene. 

Name                | StaticFrameSyncBehaviourID |
--------------------| -------------------------- |
Ball                | 1                          |
Paddle for player 1 | 2                          |
Paddle for player 2 | 3                          |

![img](./../../assets/tutorial/AddStaticFrameSync.PNG){: width=720 }