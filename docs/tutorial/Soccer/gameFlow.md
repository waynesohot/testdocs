# **Game Flow**

Next, you'll implment the game flow logic.

- Add a new Empty GameObject and name it `GameFlow`
- Add a new script called `SoccerGameFlow` to the `GameFlow` GameObject.

- Replace the contents of the file with the following. 

=== "C#"
    ``` c#
    using SocketWeaver.FrameSync;
    using SocketWeaver.FixedMath;
    using UnityEngine;
    using UnityEngine.UI;
    using SocketWeaver.FPhysics3D;
    using SocketWeaver.Core;

    namespace SWExample.Soccer
    {
        public class SoccerGameFlow : MonoBehaviour
        {
            [Header("Scores")]
            public int player1Score;
            public int player2Score;

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