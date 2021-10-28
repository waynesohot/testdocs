# **Ball Manager**

Next, you'll implment the game flow logic.

- Add a new script called `BallManager` to the `Ball` GameObject.

- Replace the content of the script with the following. Note that the BallManager implements the `IFrameSyncComputerUpdate` interface.

- Drag the `FTransform` component and the `FRigibody2D` component of the Ball GameObject to the `ballTransform` and `ballRigidbody` field.

=== "C#"
    ``` c#
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;
    using SocketWeaver.FPhysics2D;
    using UnityEngine;

    namespace SWExample.Pong
    {
        public class BallManager : MonoBehaviour, IFrameSyncComputerUpdate
        {
            public bool player1Ready = false;
            public bool player2Ready = false;

            public int player1Score = 0;
            public int player2Score = 0;

            public FFloat ballInitialSpeed = FFloat.FromDivision(5, 1);
            public FFloat ballInitialSpeedXYRatio = FFloat.three;

            public FFloat boundary = FFloat.FromDivision(11, 1);
            public FTransform ballTransform;
            public FRigidbody2D ballRigidbody;

            public void OnComputerUpdate(FrameSyncGame game, FrameSyncUpdateType frameSyncUpdateType)
            {
                //check boundary for every FrameSync frame.
                if (ballTransform.position.x < -boundary)
                {
                    //player 2 scored
                    player2Score++;
                    ResetBall();

                }
                else if (ballTransform.position.x > boundary)
                {
                    //player 1 scored
                    player1Score++;
                    ResetBall();
                }
            }

            public void PlayerIsReady(FrameSyncPlayer player)
            {
                Debug.Log($"PlayerIsReady player={player.playerId}");

                if (player.playerId == 1)
                {
                    player1Ready = true;
                }
                else
                {
                    player2Ready = true;
                }

                // fire the ball when both players are ready.
                if (player1Ready && player2Ready)
                {
                    Kickoff();
                }
            }

            void Kickoff()
            {
                // you create two random numbers in range -1 to 1 using the FrameSyncRandom.Range method. 
                // The FrameSyncRandom API generates deterministic random numbers so players will get the same random numbers across the network.
                FFloat x = FrameSyncRandom.Range(FFloat.negOne, FFloat.one) * ballInitialSpeedXYRatio;
                FFloat y = FrameSyncRandom.Range(FFloat.negOne, FFloat.one);

                // use the random numbers to calculate the initial velocity of the ball.
                FVector2 direction = new FVector2(x, y);

                Debug.Log($"Kickoff direction={direction}");

                ballRigidbody.velocity = direction.normalized * ballInitialSpeed;
            }

            void ResetBall()
            {
                // reset ball position and velocities.
                ballTransform.position = FVector3.zero;
                ballTransform.Teleport(FVector3.zero);
                ballRigidbody.velocity = FVector2.zero;
                ballRigidbody.angularVelocity = FFloat.zero;

                // reset players ready flag. So they have to press the ready button again to continue.
                player1Ready = false;
                player2Ready = false;
            }
        }
    }

    ```