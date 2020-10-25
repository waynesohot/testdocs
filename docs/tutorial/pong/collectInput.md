# Collecting Player Inputs

>> `OnCollectLocalPlayerInputs` 
Called every frame to collect the inputs of the local player.

In `OnCollectLocalPlayerInputs`, you read player inputs from the Unity `Input` class and pass it to `FrameSyncInput`.

Go to `ProjectSettings->Input manager` and add a new input `Vertical1`. You can **Right-Click** the input `Vertical` and `Duplicate Array Element` to copy the input settings. Set `Negative Button` to `down` and `Positive Button` to `up` for the new input.

![img](./../../assets/tutorial/InputSettings_Pong.PNG){: width=720 }

=== "C#"
    ``` c#
    public override void OnCollectLocalPlayerInputs(FrameSyncInput input, FrameSyncGame game)
    {
        // 1
        input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical"), player1);
        input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.G), player1);

        // 2
        input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical1"), player2);
        input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.H), player2);
    }
    ```

In `// 1`, player1 uses `w` and `s` to move and uses `g` to trigger the `ready` input.

In `// 2`, player2 uses `up arrow` and `down arrow` to move and uses `h` to trigger the `ready` input.


