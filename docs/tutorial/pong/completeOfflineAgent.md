# Complete Offline FrameSyncAgent 

The MyFrameSyncAgent.cs script should look like.

=== "C#"
    ``` c#
    using UnityEngine;
    using SWNetwork.FrameSync;
    using Parallel;

    public class MyGameSettings
    {
        public byte player1ID;
        public byte player2ID;
    }

    public class MyFrameSyncAgent : FrameSyncAgent
    {
        public SWFrameSyncPlayer player1;
        public SWFrameSyncPlayer player2;

        public override void OnFrameSyncEngineCreated(SWFrameSyncEngine engine)
        {
            // 1
            SWFrameSyncInputSetting[] inputSettings = new SWFrameSyncInputSetting[2];

            inputSettings[0] = SWFrameSyncInputSetting.CompressedFloatInput(
                                                                "y",
                                                                Fix64.FromDivision(-1, 1),
                                                                Fix64.FromDivision(1, 1),
                                                                Fix64.FromDivision(1, 10),
                                                                Fix64.zero);

            inputSettings[1] = SWFrameSyncInputSetting.TriggerInput("ready");

            SWFrameSyncInputConfig inputConfig = new SWFrameSyncInputConfig(inputSettings);
            engine.SetFrameSyncInputConfig(inputConfig);
        }

        public override void OnFrameSyncGameCreated(SWFrameSyncGame game, SWFrameSyncReplay replay)
        {
            // 1
            game.type = SWFrameSyncGameType.Offline;

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

        public override void OnCollectLocalPlayerInputs(SWFrameSyncInput input, SWFrameSyncGame game)
        {
            // 1
            input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical"), player1);
            input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.G), player1);

            // 2
            input.SetFloatForPlayer("y", (Fix64)Input.GetAxis("Vertical1"), player2);
            input.SetTriggerForPlayer("ready", Input.GetKeyUp(KeyCode.H), player2);
        }
    }
    ```