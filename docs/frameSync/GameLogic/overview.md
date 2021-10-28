# **Overview**

## **Seperation of Game Logic And Presentation**
Your game logic should only be implemented in the IFrameSync interfaces. All the Unity MonoBehaviour [events/messages][1] are considered indeterministic, you should use them for presentation only.


| **Deterministic**       |        **Description**          |
| ----------- | ------------------------------------ |
| [IFrameSyncOnStart][2]       |  Called before the first [IFrameSyncPlayerUpdate][3] and [IFrameSyncComputerUpdate][4] . Implement this interface to initialzie the component.  |
| [IFrameSyncPlayerUpdate][3]       |  Called by the `FrameSyncEngine` to update the player owned `FrameSyncBehaviour` during frame simulation.  |
| [IFrameSyncComputerUpdate][4]       |  Called by the `FrameSyncEngine` to update the computer owned `FrameSyncBehaviour` during frame simulation.  |
| [IFrameSyncTimerEventHandler][5]       |  Called when a `FrameSyncTimer` event occurs.  |

| **Indeterministic**       |        **Description**          |
| ----------- | ------------------------------------ |
| Start      |  called when the GameObject begins to exist (either when the Scene is loaded, or the GameObject is instantiated).  |
| Update      |  called every frame.  |
| FixedUpdate     |  called every physics timestep.  |
| OnCollisionEnter and OnTriggerEnter   |  called when physics collisions or triggers occur.  |

## **Networked Input**
Before the frame simulation starts, the `FrameSyncEngine` reads the input data of the frame and assign the input values to the players. 

During a frame simulaiton, the `FrameSyncEngine` updates the `FrameSyncBehaviour`s and your IFrameSyncPlayerUpdate MonoBehaivours will be updated. The player that owns the `FrameSyncBehaviour` will be passed into the `OnPlayerUpdate()` method. You can read the inputs of the player by calling `player.GetInput{InputName}()`;

???+ info

    The `player.GetInput{InputName}()` method is generated when you save the InputSettings of the game.
    See [InputSettings][6] for more details.

## **Example Script Showing The Seperation of Game Logic And Presentation**
=== "C#"
    ``` c#
    public class MyExampleScript : MonoBehaviour, IFrameSyncOnStart, IFrameSyncPlayerUpdate
    {
        //Displays player's score in a label, not used in the Game Logic
        public Text playerScoreLabel;

        //the player score, this value is used in the Game Logic
        int playerScore

        //==========Unity Events==========
        //only used to read playerScore and update the playerScoreLabel
        void Update()
        {
            playerScoreLabel.text = playerScore.ToString();
        }

        //==========Game Logic==========
        //IFrameSyncOnStart
        //used for initialize the component
        public void OnStart(FrameSyncBehaviour frameSyncBehaviour)
        {
            playerScore = 0;
        }

        //IFrameSyncPlayerUpdate
        //used to read player input and change player score
        public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncGame game, FrameSyncUpdateType frameSyncUpdateType)
        {
            bool addScore = player.GetInputAddScore();

            if(addScore)
            {
                playerScore++;
            }
        }
    }
    ```

[1]: https://docs.unity3d.com/Manual/class-MonoBehaviour.html
[2]: IFrameSyncOnStart.md
[3]: IFrameSyncPlayerUpdate.md
[4]: IFrameSyncComputerUpdate.md
[5]: IFrameSyncTimerEventHandler.md
[6]: ../InputSettings.md