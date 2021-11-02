# **Camera Target Selector**

In this section, you will create a camera target selector that selects the local player as the target of the `SoccerCameraFollow` component.

- Add a `StaticFrameSyncBehaviour` component to the `Main Camera`.
- Set the `Frame Sync Owner` of the `StaticFrameSyncBehaviour` to `Computer`.
- Create a new script and name it `CameraTargetSelector`.
- Replace the contents of the file with the following:

=== "C#"
    ``` c#
    using SocketWeaver.FixedMath;
    using SocketWeaver.FrameSync;
    using UnityEngine;

    namespace SWExample.Soccer
    {
        public class CameraTargetSelector : MonoBehaviour, IFrameSyncComputerUpdate
        {
            public FTransform player1;
            public FTransform player2;
            public SoccerCameraFollow cameraFollow;
            public bool offline = false;

            public void OnComputerUpdate(FrameSyncGame game)
            {
                if (offline)
                {
                    cameraFollow.SetTarget(player1.transform);
                }

                if (game.localPlayer == null)
                {
                    return;
                }

                if (game.localPlayer.playerId == 1)
                {
                    cameraFollow.SetTarget(player1.transform);
                }
                else
                {
                    cameraFollow.SetTarget(player2.transform);
                }
            }
        }

    }
    ```

- Drag the `SoccerCameraFollow` to `Camera Follow` field of the `CameraTargetSelector`.