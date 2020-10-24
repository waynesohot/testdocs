# Configuring the FrameSyncEngine

>> ``OnFrameSyncEngineCreated(SWFrameSyncEngine engine)`` Called after the `FrameSyncAgent` created its `FrameSyncEngine` in the ``Awake()`` method.

In `OnFrameSyncEngineCreated`, you tell the `FrameSyncEngine` what the inputs are used in your game. 

=== "C#"
    ``` c#
    public override void OnFrameSyncEngineCreated(SWFrameSyncEngine engine)
    {
        // 1
        SWFrameSyncInputSetting[] inputSettings = new SWFrameSyncInputSetting[2];

        // 2
        inputSettings[0] = SWFrameSyncInputSetting.CompressedFloatInput(
                                                               "y", 
                                                               Fix64.FromDivision(-1, 1), 
                                                               Fix64.FromDivision(1, 1), 
                                                               Fix64.FromDivision(1, 10), 
                                                               Fix64.zero);

        // 3
        inputSettings[1] = SWFrameSyncInputSetting.TriggerInput("ready");

        // 4
        SWFrameSyncInputConfig inputConfig = new SWFrameSyncInputConfig(inputSettings);
        engine.SetFrameSyncInputConfig(inputConfig);
    }
    ```
In `// 1`, you create an array of input settings, the game uses 2 inputs, so the array size is 2.

In `// 2`, the first input is a `CompressedFloatInput`. it contains the information of the vertical axes from the keyboard. you will feed player's input to it later when we implement the `OnCollectLocalPlayerInputs` method.

In `// 3`, the second input is a `TriggerInput`, players will trigger this input when they are ready to play the game.

In `// 4`, you use the input settings array to create an `inputConfig` and you pass it to the `FrameSyncEngine` using the `SetFrameSyncInputConfig` method.

[1]: ../../frameSync/importantClass/frameSyncAgent.md