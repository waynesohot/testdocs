# **Overview**

A library for creating real-time multiplayer games with Unity. The library exchanges and manages players inputs. The synchronization of game states is achieved based on full deterministic simulation. The library verifies the simulation results of players in the same room to prevent cheating and desyncs.

## **Advantages**

- **Low bandwidth usage**: scales as the size of the inputs and the number of players
- **Networked physics**: works out of the box with our 2D and 3D physics engine.
- **Cheat prevention**: simulation results are hashed and compared periodically.
- **Lag compensation**: responsive gameplay when running in the prediction/rollback mode.

## **Offline Mode**
Designed for local split screen games and single player mode, also useful for developing games offline.

## **Lockstep Mode**
Designed for RTS, MOBA games that a lot of gameobjects need to be synchronized. 

## **Prediction/Rollback Mode**
Designed for vehicle simulation, Fighting and FPS games that are fast-paced and sensitive to network latency.