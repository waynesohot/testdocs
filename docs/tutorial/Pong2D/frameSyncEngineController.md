# **FrameSyncEngineController**

The FrameSyncEngine is the core of the FrameSync library. You will create a subclass of the built-in `FrameSyncEngineController` to control the FrameSyncEninge.

- Create a new script and name it `PongFrameSyncEngineController`.
- Create a new empty GameObject and attach the `PongFrameSyncEngineController` to it.
- In the `PongFrameSyncEngineController` script, remove `Start()` and `Update` and add the following code.
- Drag the `FPhysics2DManager` into the physicsEngine field in the inspector.

=== "C#"
    ``` c#
    using UnityEngine;
    using SocketWeaver.FrameSync;
    using SocketWeaver.FPhysics2D;
    using SocketWeaver.FixedMath;

    namespace SWExample.Pong
    {
        public class PongFrameSyncEngineController : FrameSyncEngineController
        {
            //reference to the FPhysics2DManager
            public FPhysics2DManager physicsEngine;

            //Called when the FrameSyncEngine samples the inputs of the local player
            protected override void OnFrameSyncCollectPlayerInput(FrameSyncEngine frameSyncEngine, FrameSyncGame game)
            {
                //set the inputs for the local player
                game.localPlayer.SetInputY((FFloat)Input.GetAxis("Vertical"));
                game.localPlayer.SetInputReady(Input.GetKeyUp(KeyCode.G));
            }

            protected override void OnStart()
            {
                //manually initialize the physics engine
                physicsEngine.Initialize();
            }

            //Called after the StaticFrameSyncBehaviours and the DynamicFrameSyncBehaviours
            //finished simulation for the current FrameSync step
            protected override void OnFrameSyncFinishedSimulationForCurrentFrame(int frameNumber)
            {
                //manually update the physics engine
                physicsEngine.OnUpdate(FrameSyncTime.fixedDeltaTime);
            }
        }
    }

    ```