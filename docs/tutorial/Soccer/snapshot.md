# **Game States Snapshot**

In this seciton, you will take snapshots the game states to support running the game in the Prediction/Rollback mode.

## **Identify Game States That Should Be in The Snapshot**

### **External States**
The rigidbodies physics states like position, rotation, linear velocity, angular velocity are stored in the physics engine. They should be exported for rollback.

### **FrameSyncBehaviour States**

Name    | Export | Description
--------| --------- | ----------------
SoccerVehicleController    | No   | The vehicle physics states is stored in the physics engine. The component itself is stateless.
SoccerGoal | No | The trigger states: enter, stay, exit is stored in the physics engine. The component itself is stateless.
SoccerGameFlow   | Yes     | The component is stateful. We should snapshot the player scores and timer Id.

## **Physics Engine Snapshot**

### **SoccerPhysics3DSnapshot**

You will use the following methods to create snapshot of the physics engine.

Name    | Description
--------| --------- 
FPhysics3D.Snapshot    | Create a snapshot of the physics engine's current states
FPhysics3D.ImportSnapshot    | Create a snapshot using the given byte data

You will use the following method to restore the physics engine to a snapshot.

Name    | Description
--------| --------- 
FPhysics3D.Restore    | Restore the physics engine to a snapshot

You will use the following method to export the data of a snapshot in the byte array format.

Name    | Description
--------| --------- 
FPhysics3D.ExportSnapshot    | Export the data of a snapshot in byte array format.


Create a new c# script and call it `SoccerPhysics3DSnapshot`.

Replace the content of the file with the following.

=== "C#"
    ``` c#
    using SocketWeaver.FrameSync;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.Core;

    public class SoccerPhysics3DSnapshot : IFrameSyncSnapshot
    {
        FSnapshot3D snapshot;

        public int frameNumber { get; }

        public SoccerPhysics3DSnapshot(int frameNumber)
        {
            snapshot = FPhysics3D.Snapshot();
            this.frameNumber = frameNumber;
        }

        public SoccerPhysics3DSnapshot(int frameNumber, byte[] bytes)
        {
            snapshot = FPhysics3D.ImportSnapshot(bytes, bytes.Length);
            this.frameNumber = frameNumber;
        }

        public void Clear()
        {
            if (snapshot != null)
            {
                FPhysics3D.DestroySnapshot(snapshot);
                snapshot = null;
            }
        }

        public SWBytes Export()
        {
            byte[] bytes = new byte[1014];

            int size = FPhysics3D.ExportSnapshot(snapshot, bytes, 1024);

            SWBytes b = new SWBytes(size);

            b.Push(bytes, size);

            return b;
        }

        public void Restore()
        {
            FPhysics3D.Restore(snapshot);
        }
    }

    ```

Add the highlighted code to the SoccerFrameSyncEngineController.

=== "C#"
    ``` c# hl_lines="38-46"
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

            protected override IFrameSyncSnapshot OnFrameSyncCreateCustomRestorable(int frameNumber)
            {
                return new PhysicsSnapshot(frameNumber);
            }

            protected override IFrameSyncSnapshot OnFrameSyncImportCustomRestorable(int frameNumber, byte[] bytes)
            {
                return new PhysicsSnapshot(frameNumber, bytes);
            }
        }
    }

    ```

## **SoccerGameFlow Snapshot**