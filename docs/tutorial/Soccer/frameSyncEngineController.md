# **FrameSyncEngineController**

In this section, you will create a subclass of the built-in FrameSyncEngineController to control the FrameSyncEninge.

- Create a new script and name it `SoccerFrameSyncEngineController`.
- Create a new empty GameObject and attach the `SoccerFrameSyncEngineController` to it.
- In the `SoccerFrameSyncEngineController` script, replace its contents with the following.
- Drag the `FPhysics3DManager` into the physicsEngine field in the inspector.

=== "C#"
    ``` c#
    using SocketWeaver.FrameSync;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.FixedMath;
    using UnityEngine;

    namespace SWExample.Soccer
    {
        public class SoccerFrameSyncEngineController : FrameSyncEngineController
        {
            public FPhysics3DManager physicsEngine;

            protected override void OnFrameSyncCollectPlayerInput(FrameSyncEngine frameSyncEngine, FrameSyncGame game)
            {
                if (engineMode == EngineMode.Offline)
                {
                    FrameSyncPlayer player1 = game.GetPlayer(1);

                    player1.SetInputX((FFloat)Input.GetAxis("Horizontal"));
                    player1.SetInputY((FFloat)Input.GetAxis("Vertical"));
                }
                else
                {
                    frameSyncEngine.game.localPlayer.SetInputX((FFloat)Input.GetAxis("Horizontal"));
                    frameSyncEngine.game.localPlayer.SetInputY((FFloat)Input.GetAxis("Vertical"));
                }
            }

            protected override void OnStart()
            {
                physicsEngine.Initialize();
            }

            protected override void OnFrameSyncFinishedSimulationForCurrentFrame(int frameNumber)
            {
                physicsEngine.OnUpdate(FrameSyncTime.fixedDeltaTime);
            }
        }
    }

    ```