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
        // offline players
        public SWFrameSyncPlayer player1;
        public SWFrameSyncPlayer player2;

        // physics controller of the scene
        ParallelPhysicsController2D parallelPhysics;

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

            // 5
            parallelPhysics = FindObjectOfType<ParallelPhysicsController2D>();
            parallelPhysics.autoUpdate = false;

            engine.OnEngineWillSimulateEvent += FrameSyncEngineWillSimulate;
        }

        void FrameSyncEngineWillSimulate()
        {
            // 6
            parallelPhysics.Step(FrameSyncTime.fixedDeltaTime);
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