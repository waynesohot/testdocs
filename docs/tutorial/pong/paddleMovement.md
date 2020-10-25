# Paddle Movement

Next, you'll implement the paddle movement logic.

Add a new script called `PaddleUpdate` to the `Paddle` GameObject. 

Replace the content of the script with the following. Note that the `PaddleUpdate` implements the `IFrameSyncUpdate` interface.

=== "C#"
    ``` c#
    using UnityEngine;
    using SWNetwork.FrameSync;
    using Parallel;

    public class PaddleUpdate : MonoBehaviour, IFrameSyncUpdate
    {
        // movement speed of the paddle
        public Fix64 speed = Fix64.FromDivision(5, 1);

        // reference to the PaddleOwnerData component
        PaddleOwnerData ownerData;

        // reference to the ParallelTransform component
        ParallelTransform parallelTransform;

        public void Awake()
        {
            ownerData = GetComponent<PaddleOwnerData>();
            parallelTransform = GetComponent<ParallelTransform>();
        }

        public void FrameSyncUpdate(FrameSyncInput input, FrameSyncUpdateType frameSyncUpdateType)
        {
        }
    }
    ```

## FrameSyncUpdate

Add the following to the `FrameSyncUpdate` method.

=== "C#"
    ``` c#
    public void FrameSyncUpdate(FrameSyncInput input, FrameSyncUpdateType frameSyncUpdateType)
    {
        // 1
        Fix64 y = input.GetFloatForPlayer("y", ownerData.player);

        // 2
        Fix64Vec3 displacement = speed * FrameSyncTime.fixedDeltaTime * new Fix64Vec3(Fix64.zero, y, Fix64.zero);
        parallelTransform.position += displacement;
    }
    ```
In `// 1`, you read the `y` input of the paddle owner player.

In `// 2`, you calculate the displacement for the frame and update the position of the paddle.