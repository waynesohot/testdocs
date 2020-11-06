# Online FrameSyncAgent

You'll modify the MyFrameSyncAgent script to support playing the game online.

First, add a public field `offline` to the `MyFrameSyncAgent` script to control **online/offline** mode in the inspector

=== "C#"
    ``` c#
    public bool offline = false;
    ```

## Updating the OnFrameSyncEngineCreated method

Next, you'll configure the networking input/output of the engine by adding `// 7` to the `OnFrameSyncEngineCreated` method.

=== "C#"
    ``` c#
        public override void OnFrameSyncEngineCreated(FrameSyncEngine engine)
    {
        // 1
        FrameSyncInputSetting[] inputSettings = new FrameSyncInputSetting[2];

        // 2
        inputSettings[0] = FrameSyncInputSetting.CompressedFloatInput(
                                                               "y",
                                                               Fix64.FromDivision(-1, 1),
                                                               Fix64.FromDivision(1, 1),
                                                               Fix64.FromDivision(1, 10),
                                                               Fix64.zero);

        // 3
        inputSettings[1] = FrameSyncInputSetting.TriggerInput("ready");

        // 4
        FrameSyncInputConfig inputConfig = new FrameSyncInputConfig(inputSettings);
        engine.SetFrameSyncInputConfig(inputConfig);

        // 5
        parallelPhysics = FindObjectOfType<ParallelPhysicsController2D>();
        parallelPhysics.autoUpdate = false;

        // 6
        engine.OnEngineWillSimulateEvent += FrameSyncEngineWillSimulate;

        // 7
        if(!offline)
        {
            engine.SetNetworkIO(FrameSyncClient.Instance.frameSyncIO);
        }
    }
    ```

## Updating the OnFrameSyncGameCreated method

Replace the content of the `OnFrameSyncGameCreated` method with the following.

=== "C#"
    ``` c#
        public override void OnFrameSyncGameCreated(FrameSyncGame game, FrameSyncReplay replay)
    {
        if (offline)
        {
            // 1
            game.type = FrameSyncGameType.Offline;

            // 2
            player1 = game.CreateOfflineGamePlayer();
            player2 = game.CreateOfflineGamePlayer();

            // 3
            MyGameSettings gameSettings = new MyGameSettings();
            gameSettings.player1ID = player1.PlayerID;
            gameSettings.player2ID = player2.PlayerID;

            // 4
            game.userData = gameSettings;
        }
        else
        {
            // 5
            game.type = FrameSyncGameType.Online;

            // 6
            game.SetPlayerDataProvider(FrameSyncClient.Instance.playerDataProvider);
            game.CreateOnlinePlayers();

            // 7
            game.CreateGameUserData<MyGameSettings>();

            //todo: game settings will be created in the matchmaking stage
            MyGameSettings gameSettings = new MyGameSettings();
            gameSettings.player1ID = 1;
            gameSettings.player2ID = 2;
            game.userData = gameSettings;
        }
    }
    ```

In `// 5`, you set the game type to `Online`.

In `// 6`, you create the online players by setting the `PlayerDataProvider` of the game and calling the `CreateOnlinePlayers` method.

In `// 7`, you create the `userData` of the game. the `userData` is hardcoded for now for testing.

## Updating the OnCollectLocalPlayerInputs method

Replace the content of the `OnCollectLocalPlayerInputs` method with the following.

=== "C#"
    ``` c#
        public override void OnCollectLocalPlayerInputs(FrameSyncInput input, FrameSyncGame game)
    {
        if(offline)
        {
            // 1
            input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical"), player1);
            input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.G), player1);

            // 2
            input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical1"), player2);
            input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.H), player2);
        }
        else
        {
            // 3
            input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical"), game.localPlayer);
            input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.G), game.localPlayer);
        }
    }
    ```

    In `// 3`, collect input values of the `up arrow`, `down arrow`, and `g` keys for the local player.