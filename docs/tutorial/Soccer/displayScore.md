# **Display the scores**

In this section, you will update the HUD to display the scores.

- Add a `StaticFrameSyncBehaviour` to the `GameFlow` GameObject. We want to access the `FrameSyncGame` in the `SoccerGameFlow` script to get the time elapsed since the game started.
- Set the `Owner` of the `StaticFrameSyncBehaviour` to computer because the `GameFlow` is not owned by any player.
- Add the highlighted lines to the `SoccerGameFlow` script.
- Drag the `Time`, `Player1`, and `Player2` text to the SoccerGameFlow inspector.

=== "C#"
    ``` c# hl_lines="10 12-15 21-34"
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;
    using UnityEngine;
    using UnityEngine.UI;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.Core;

    namespace SWExample.Soccer
    {
        public class SoccerGameFlow : MonoBehaviour, IFrameSyncComputerUpdate
        {
            [Header("UI")]
            public Text timeText;
            public Text player1Text;
            public Text player2Text;

            [Header("Scores")]
            public int player1Score;
            public int player2Score;

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
            }
        }
    }

    ```

## **Test**
Hit **Play**, you should see the time text and the score texts are updated corretly.

![img](./../../assets/soccer/score.gif){: width=1080 }