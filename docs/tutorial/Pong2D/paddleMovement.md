# **Paddle Movement**

Next, you will implement the paddle movement logic.

- Add a new script called `PaddleMovement` to the Paddle GameObject.

- Replace the content of the script with the following. Note that the PaddleMovement implements the IFrameSyncPlayerUpdate interface.

- Drag the FTransform component of the Paddle GameObject to the PaddleMovement component.

=== "C#"
    ``` c#
    using UnityEngine;
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;

    namespace SWExample.Pong
    {
        public class PaddleMovement : MonoBehaviour, IFrameSyncPlayerUpdate
        {
            public FFloat speed = FFloat.FromDivision(5, 1);

            public FTransform fTransform;

            public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncGame game, FrameSyncUpdateType frameSyncUpdateType)
            {
                //read the y input of the paddle owner player
                FFloat y = player.GetInputY();

                //calculate the displacement for the frame
                FVector3 displacement = speed * FrameSyncTime.fixedDeltaTime * new FVector3(FFloat.zero, y, FFloat.zero);

                //update the position of the paddle
                fTransform.position += displacement;

                //read the ready input for the paddle owner player
                if(player.GetInputReady())
                {
                    //notify the BallManager that the player is ready
                    BallManager ballManager = FindObjectOfType<BallManager>();
                    
                    ballManager.PlayerIsReady(player);
                }
            }
        }
    }

    ```