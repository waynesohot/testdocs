# **Reset to The Start Position**

Now, the ball and the cars are not getting reset to their starting positions.

Add the highlighted lines to the `SoccerGameFlow` script.

=== "C#"
    ``` c# hl_lines="17-25 69 72-89"
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;
    using UnityEngine;
    using UnityEngine.UI;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.Core;

    namespace SWExample.Soccer
    {
        public class SoccerGameFlow : MonoBehaviour, IFrameSyncOnStart, IFrameSyncComputerUpdate
        {
            [Header("UI")]
            public Text timeText;
            public Text player1Text;
            public Text player2Text;

            [Header("Rigidbodies")]
            public FRigidbody3D ball;
            public FRigidbody3D player1;
            public FRigidbody3D player2;

            [Header("Start Positions")]
            public FTransform ballStartPosition;
            public FTransform player1StartPosition;
            public FTransform player2StartPosition;

            [Header("Scores")]
            public int player1Score;
            public int player2Score;

            StaticFrameSyncBehaviour _frameSyncBehaviour;

            public void OnStart(FrameSyncBehaviour frameSyncBehaviour)
            {
                _frameSyncBehaviour = frameSyncBehaviour;
            }

            public void OnComputerUpdate(FrameSyncGame game)
            {
                float elapsed = (float)game.Elapsed();

                int seconds = (int)elapsed;

                int minutes = seconds / 60;
                seconds = seconds % 60;

                timeText.text = $"{minutes.ToString("00")}:{seconds.ToString("00")}";

                player1Text.text = $"{player1Score}";
                player2Text.text = $"{player2Score}";
            }

            public void PlayerScored(FrameSyncPlayer player)
            {
                Debug.Log($"PlayerScored player={player.playerId}");

                //update player scores
        
                if (player.playerId == 1)
                {
                    player1Score++;
                }

                if (player.playerId == 2)
                {
                    player2Score++;
                }

                ResetGame();
            }

            void ResetGame()
            {
                ball.gameObject.SetActive(true);

                ResetRigidbody(ball, ballStartPosition);
                ResetRigidbody(player1, player1StartPosition);
                ResetRigidbody(player2, player2StartPosition);
            }

            void ResetRigidbody(FRigidbody3D fRigidbody3D, FTransform startPosition)
            {
                fRigidbody3D.position = startPosition.position;
                fRigidbody3D.rotation = startPosition.rotation;
                fRigidbody3D.fTransform.Teleport(startPosition.position);

                fRigidbody3D.velocity = FVector3.zero;
                fRigidbody3D.angularVelocity = FVector3.zero;
            }
        }
    }

    ```
- Drag the `Ball`, and the `Car`s into the `Rigidbodies` fields.
- Create empty GameObjects at the starting positions of the `Ball`, and the `Call`s.
- Attach `FTransform` component to the empty GameObjects.
- Drag the empty GameObjects to the `Start Positions` fields.

## **Test**
Hit **Play**, you should see that the balls and the cars get reset to their starting positions.

![img](./../../assets/soccer/testplay.gif){: width=1080 }

