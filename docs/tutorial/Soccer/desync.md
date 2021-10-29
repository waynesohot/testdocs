# **Desync Detection**

Currently, the game does not verify clients simulation results. So if the clients simulation diverged, their simulation would only get further apart from the frame the desync started.

The `FrameSyncEngine` hashes the `FrameSyncBehaviour` data once every 60 FrameSync frames. The **FrameSync** server will verify the clients checksums and notify the clients which have different simulation results from others.

In this game, the only stateful component managed by the `FrameSyncBehaviour` is the `SoccerGameFlow` component. You have implemented the `IFrameSyncDataContainer` interface to export its states so the player scores and timerId are being verified.

You also created the `SoccerPhysicsSnapshot` to take snapshots of the physics engine. To verify the physics states stay in sync, you can override the `OnFrameSyncGetExternalChecksum()` method in the `SoccerFrameSyncEngineController`.

Add the highlighted code to the `SoccerFrameSyncEngineController`. You are going to verify the positions of the Ball and the Cars using the `FrameSyncChecksum` API. Also, you are going to stop the `FrameSyncEngine` on desync.

=== "C#"
    ``` c# hl_lines="12-15 53-72"
    using SocketWeaver.FrameSync;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.FixedMath;
    using UnityEngine;

    namespace SWExample.Soccer
    {
        public class SoccerFrameSyncEngineController : FrameSyncEngineController
        {
            public FPhysics3DManager physicsEngine;

            [Header("checksum")]
            public FTransform ball;
            public FTransform player1;
            public FTransform player2;

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

            protected override IFrameSyncSnapshot OnFrameSyncCreateCustomSnapshot(int frameNumber)
            {
                return new PhysicsSnapshot(frameNumber);
            }

            protected override IFrameSyncSnapshot OnFrameSyncImportCustomSnapshot(int frameNumber, byte[] bytes)
            {
                return new PhysicsSnapshot(frameNumber, bytes);
            }

            protected override uint OnFrameSyncGetCustomHashCode()
            {
                using (FrameSyncChecksum checksum = FrameSyncChecksum.Instance)
                {
                    //If velocities are out of sync,
                    //Positions should be out of sync as well. 
                    //So we are only verifying positions. 
                    checksum.Add(ball.position);
                    checksum.Add(player1.position);
                    checksum.Add(player2.position);

                    return checksum.value;
                }
            }

            protected override FrameSyncRestoreMethod OnFrameSyncDesyncDetected(FrameSyncDesyncInfo desyncInfo)
            {
                Debug.LogError("Desync!");
                return FrameSyncRestoreMethod.Abort;
            }
        }
    }

    ```

