# Configuring the FrameSyncGame

>> `OnFrameSyncGameCreated`
Called after the `FrameSyncAgent` created its `FrameSyncGame` in the `Awake()` method.

In `OnFrameSyncGameCreated`, you create the players and set the game custom data of your game.

=== "C#"
    ``` c#
    public class MyGameSettings
    {
        public byte player1ID;
        public byte player2ID;
    }
    ```

You will use `MyGameSettings` as the custom data of your game. 

In online mode, game custom data is configured in the matchmaking stage before creating the `FrameSyncAgent`. 

For now, you will hardcode it to run the game offline.

=== "C#"
    ``` c#
    public override void OnFrameSyncGameCreated(FrameSyncGame game, FrameSyncReplay replay)
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
    ```
In `// 1`, you set the game type to offline.

In `// 2`, you created two offline players.

In `// 3`, you created a `MyGameSettings` object and set its playerIDs to the offline players you just created in `// 2`.

In `// 4`, you passed the `MyGameSettings` Object created in `// 3` to the `FrameSyncGame`.