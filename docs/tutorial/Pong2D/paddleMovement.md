# **Paddle Movement**

Next, you will implement the paddle movement logic.

Add a new script called `PaddleMovement` to the Paddle GameObject.

Replace the content of the script with the following. Note that the PaddleMovement implements the IFrameSyncPlayerUpdate interface.

=== "C#"
    ``` c#
    using UnityEngine;
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;

    namespace SWExample.Pong
    {
        public class PaddleMovement : FrameSyncEngineController
        {
            public FFloat speed = FFloat.FromDivision(5, 1);

            public FTransform fTransform;

            public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncUpdateType frameSyncUpdateType)
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
                    PongBallManager pongBallManager = FindObjectOfType<PongBallManager>();
                    
                    pongBallManager.PlayerIsReady(player);
                }
            }
        }
    }

    ```