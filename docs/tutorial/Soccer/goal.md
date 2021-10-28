# **Goal**

In this section, you will implement the soccer goal logic.

- Create a new script `SoccerGoal` and add it to the `Goal` GameObject.
- Add a `StaticFrameSyncBehaviour` component to the `Goal` and set its `Own` to `Player1`.

Replace the contents in the `SoccerGoal` script with the following.

=== "C#"
    ``` c#
    using SocketWeaver.FPhysics3D;
    using UnityEngine;
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;

    namespace SWExample.Soccer
    {
        public class SoccerGoal : MonoBehaviour, IFrameSyncOnStart
        {
            StaticFrameSyncBehaviour _frameSyncBehaviour;

            public void OnStart(FrameSyncBehaviour frameSyncBehaviour)
            {
                _frameSyncBehaviour = frameSyncBehaviour;
            }

            public void OnFTriggerEnter(FCollider3D fCollider)
            {
                //score
                FrameSyncPlayer player = _frameSyncBehaviour.owner;

                GameFlow gameFlow = FindObjectOfType<GameFlow>();

                gameFlow.PlayerScored(player);
            }
        }
    }

    ```

## **Trigger events**

To enable trigger events of the `Goal` collider:

- Enabled `Collision Events` of the `FRigidbody3D` component of the `Goal` GameObject
- Add an event listener to the `OnTriggerEnter` event, and select `OnFTriggerEnter`. 

## **Physics Layer Settings**

FPhysics supports the Unity physics layer settings. 

Create the following layers and assign car, ball and goal to their layers

Layer Name     | GameObject | Description
--------| --------- | ----------------
SoccerBall    | Ball   | Collides with the cars, the goals, and the Arena   
SocerCars | Cars | Collides with other cars, the ball, and the Arena
SoccerGoal   | Goals     | Collides with the ball only  
