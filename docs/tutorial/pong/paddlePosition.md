# Paddle Position Data

Next, you'll export the paddle position data. The paddle position should be exported and uploaded to the game server for validation.

Add a new script called `PaddlePositionData` to the `Paddle` GameObject. 

Replace the content of the script with the following. Note that the `PaddlePositionData` implements the `IFrameSyncData` interface.

=== "C#"
    ``` c#
    using UnityEngine;
    using SWNetwork.FrameSync;
    using SWNetwork.Core;
    using System.Collections.Generic;
    using Parallel;

    public class PaddlePositionData : MonoBehaviour, IFrameSyncData
    {
        // reference to the PaddleOwnerData component
        ParallelTransform parallelTransform;

        public void Awake()
        {
            parallelTransform = GetComponent<ParallelTransform>();
        }

        public void FrameSyncDataInitialize(SWFrameSyncGame game)
        {

        }

        public void Import(SWBytes buffer)
        {
        }

        public void Export(SWBytes buffer)
        {
        }

        public void ExportDebugInfo(Dictionary<string, string> debugDictionary)
        {
        }
    }
    ```

## Importing

Add the following to the `Import` methods.

=== "C#"
    ``` c#
    public void Import(SWBytes buffer)
    {
        // 1
        long y = buffer.PopLong();
        Fix64 fy = Fix64.FromRaw(y);

        // 2
        parallelTransform.position = new Fix64Vec3(
                                            parallelTransform.position.x, 
                                            fy, 
                                            parallelTransform.position.z);
    }
    ```

In `// 1`, you pop the `y` position value from the buffer.

In `// 2`, you restore the paddle position to the `y` position value.

## Exporting

Add the following to the `Export` methods.

=== "C#"
    ``` c#
    public void Export(SWBytes buffer)
    {
        // 1
        buffer.Push(parallelTransform.position.y.Raw);
    }
    ```

In `// 1`, you push the `y` position value to the buffer.

???+ info
    The `ExportDebugInfo` method is left empty. It is only used when you are debugging the game with a local dev server.