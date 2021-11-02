# **StaticFrameSyncBehaviour**

The `StaticFrameSyncBehaviour` is the unique identifier of a GameObject. It helps the FrameSyncEngine to identify a networked GameObjec.

## **Which GameObjects should have a StaticFrameSyncBehaviour?**

You have the following Rigidbodies active in the game. 

Name    | Body Type | Description
--------| --------- | ----------------
Ball    | Dynamic   | Controlled by physics
Paddles | Kinematic | Controlled by players
Walls   | Staic     | Do not move


- For the Paddles, they read player inputs to move and their position is networked, so we should add `StaticFrameSyncBehaviour` to them.

- For the Ball, its position is updated by physics and is networked. so it should have a `StaticFrameSyncBehaviour`.

- For the Walls, they do not move and their states do not change so we do not need to add `StaticFrameSyncBehaviour` to them.

## **Adding the StaticFrameSyncBehaviour component**

- Select the `Ball` and the `Paddle`s in the `Hierarchy` window and add `StaticFrameSyncBehaviour` to them by selecting `Add Component`->`Static Frame Sync Behaviour`.

## **StaticFrameSyncBehaviour Owner**

- Select the left paddle and set its `Frame Sync Owner` to `player1`.
- Select the right paddle and set its `Frame Sync Owner` to `player2`.
- Select the ball and set its `Frame Sync Owner` to `computer`.