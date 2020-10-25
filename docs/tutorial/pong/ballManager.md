# Ball Manager

Next, you'll implment the game flow logic.

Add a new script called `BallManager` to the `Ball` GameObject. 

Replace the content of the script with the following. Note that the `BallManager` implements the `IFrameSyncData` interface and the `IFrameSyncUpdate` interface.

=== "C#"
    ``` c#
    using System.Collections.Generic;
    using UnityEngine;
    using SWNetwork.FrameSync;
    using Parallel;
    using SWNetwork.Core;

    public class BallManager : MonoBehaviour, IFrameSyncUpdate, IFrameSyncData
    {
        public bool player1Ready = false;
        public bool player2Ready = false;

        public int player1Score = 0;
        public int player2Score = 0;

        public Fix64 ballInitialSpeed = Fix64.FromDivision(5, 1);

        // reference to the ball's ParallelTransform component
        ParallelTransform parallelTransform;

        // reference to the ball's ParallelRigidbody2D component
        ParallelRigidbody2D parallelRigidbody2D;

        public void Awake()
        {
            parallelTransform = GetComponent<ParallelTransform>();
            parallelRigidbody2D = GetComponent<ParallelRigidbody2D>();
        }

        public void FrameSyncUpdate(FrameSyncInput input, FrameSyncUpdateType frameSyncUpdateType)
        {
        }

        public void FrameSyncDataInitialize(FrameSyncGame game)
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

## Kickoff

The Game starts when both player1 and player2 have pressed the `ready` button.

Add the following methods to the `BallManager` script.

=== "C#"
    ``` c#
    public void PlayerIsReady(PaddleOwnerData.PaddleOwner owner)
    {
        // 1
        if (owner == PaddleOwnerData.PaddleOwner.Player1)
        {
            player1Ready = true;
        }
        else
        {
            player2Ready = true;
        }

        // 2
        if (player1Ready && player2Ready)
        {
            Kickoff();
        }
    }

    public void Kickoff()
    {
        // 3
        Fix64 x = FrameSyncRandom.Range(Fix64.NegOne, Fix64.one);
        Fix64 y = FrameSyncRandom.Range(Fix64.NegOne, Fix64.one);

        // 4
        Fix64Vec2 direction = new Fix64Vec2(x, y);
        parallelRigidbody2D.LinearVelocity = direction.normalized * ballInitialSpeed;
    }
    ```
In `// 1`, you set player1 and player2 ready based on the `owner` parameter.

In `// 2`, you fire the ball when both players are ready.

In `// 3`, you create two random numbers in range `-1` to `1` using the `FrameSyncRandom.Range` method. The `FrameSyncRandom` class generates deterministic random numbers so players will get the same random numbers across the network.

In `// 4`, you use the random numbers to calculate the initial velocity of the ball.

### Handle player ready input

Add the following to the `PaddleUpdate` script

=== "C#"
    ``` c#
    public void FrameSyncUpdate(FrameSyncInput input, FrameSyncUpdateType frameSyncUpdateType)
    {
        // 1
        Fix64 y = input.GetFloatForPlayer("y", ownerData.player);

        // 2
        Fix64Vec3 displacement = speed * FrameSyncTime.fixedDeltaTime * new Fix64Vec3(Fix64.zero, y, Fix64.zero);
        parallelTransform.position += displacement;

        // 3
        if (input.GetTriggerForPlayer("ready", ownerData.player))
        {
            BallManager ballManager = FindObjectOfType<BallManager>();
            ballManager.PlayerIsReady(ownerData.owner);
        }
    }
    ```

In `// 3`, you read the `ready` input for the paddle owner player and tells the `BallManager` that the player is ready.

## Boundary Check

Add the following to the `FrameSyncUpdate` method in the `BallManager` script.

=== "C#"
    ``` c#
    public void FrameSyncUpdate(FrameSyncInput input, FrameSyncUpdateType frameSyncUpdateType)
    {
        //check boundary
        if (parallelTransform.position.x < Fix64.FromDivision(-11, 1))
        {
            //player 2 scored
            player2Score++;
            ResetBall();

        }
        else if (parallelTransform.position.x > Fix64.FromDivision(11, 1))
        {
            //player 1 scored
            player1Score++;
            ResetBall();
        }
    }
    ```
For every FrameSync frame, you check if the ball is out of the boundary. 

- If the ball has passed the player1's paddle, player2 scores. 

- If the ball passed the player2's paddle, player1 scores.

### Reset the ball

Add a new method `ResetBall`

=== "C#"
    ``` c#
    public void ResetBall()
    {
        // 1
        parallelTransform.position = Fix64Vec3.zero;
        parallelRigidbody2D.LinearVelocity = Fix64Vec2.zero;
        parallelRigidbody2D.AngularVelocity = Fix64.zero;

        // 2
        player1Ready = false;
        player2Ready = false;
    }
    ```

In `// 1`, you reset ball's position and velocities.

In `// 2`, you reset players ready flag. So the players have to press the `ready` button again to continue.