# **IFrameSyncSnapshot**

## Declaration
=== "C#"
    ``` c#
    public interface IFrameSyncSnapshot
    {
        void Restore();
        void Clear();
        SWBytes Export();
    }
    ```

## **Description**

Designed for game states that are not owned by a `FrameSyncBehaviour`. For game states owned by a `FrameSyncBehaviour`, implement 
[IFrameSyncDataContainer][1] in a `MonoBehaviour` component and attach it to the GameObject.

## **Example**
In this example, we created `Physics2DSnapshot` that implements the `IFrameSyncSnapshot` interface.

=== "C#"
    ``` c#
    public class Physics2DSnapshot : IFrameSyncSnapshot
    {
        FSnapshot2D snapshot2D;

        public int frameNumber { get; }

        public Physics2DSnapshot(int frameNumber)
        {
            snapshot2D = FPhysics2D.Snapshot();
            this.frameNumber = frameNumber;
        }

        public Physics2DSnapshot(int frameNumber, byte[] bytes)
        {
            snapshot2D = FPhysics2D.ImportSnapshot(bytes, bytes.Length);
            this.frameNumber = frameNumber;
        }

        //=============== IFrameSyncSnapshot ===============
        
        //FrameSyncEngine won't need this IFrameSyncSnapshot anymore.
        //release resource if necessary.
        public void Clear()
        {
            if(snapshot2D != null)
            {
                FPhysics2D.DestroySnapshot(snapshot2D);
                snapshot2D = null;
            }
        }

        //FrameSyncEngine will restore the game states using this IFrameSyncSnapshot
        public void Restore()
        {
            FPhysics2D.Restore(snapshot2D);
        }

        //Used only when other clients need a copy of this IFrameSyncSnapshot.
        //The SWBytes will be send to the other clients to restore game states.
        //This happens:
        //1: when other clients connect to the game and need to restore game states.
        //2: when desyncs are detected on other clients.
        public SWBytes Export()
        {
            byte[] bytes = new byte[1014];

            int size = FPhysics2D.ExportSnapshot(snapshot2D, bytes, 1024);

            SWBytes b = new SWBytes(size);

            b.Push(bytes, size);

            return b;
        }


    }
    ```

The `Physics2DSnapshot` object is used by the `FrameSyncEngine` to restore the states in the `FPhysics2D` world.

=== "C#"
    ``` c#
    public class MyFrameSyncEngineController : FrameSyncEngineController
    {
        .
        .
        .

        protected override IFrameSyncSnapshot OnFrameSyncCreateCustomRestorable(int frameNumber)
        {
            return new Physics2DSnapshot(frameNumber);
        }

        protected override IFrameSyncSnapshot OnFrameSyncImportCustomRestorable(int frameNumber, byte[] bytes)
        {
            return new Physics2DSnapshot(frameNumber, bytes);
        }
    }
    ```

    [1]: IFrameSyncDataContainer.md