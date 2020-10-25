# FrameSyncAgent 
Your code interacts with the `FrameSyncEngine` and the `FrameSyncGame` by implementing a class derives from the build-in class called `FrameSyncAgent`. The `FrameSyncAgent` class is derived from the Unity `MonoBehaviour` class, and it creates a `FrameSyncEngine` and a `FrameSyncGame` in its `Awake()` method.

Example contents of a FrameSyncAgent subclass:

=== "C#"
    ``` c#
    using UnityEngine;
    using SWNetwork.FrameSync;

    public class MyFrameSyncAgent : FrameSyncAgent
    {
        public override void OnFrameSyncEngineCreated(FrameSyncEngine engine)
        {

        }

        public override void OnFrameSyncGameCreated(FrameSyncGame game, FrameSyncReplay replay)
        {

        }

        public override void OnCollectLocalPlayerInputs(FrameSyncInput input, FrameSyncGame game)
        {

        }
    }

    ```
## Events
The FrameSyncAgent class provides a collection of useful events which allows you to customize the FrameSync build-in classes for your game.

### `OnFrameSyncEngineCreated` 
Called after the FrameSyncAgent created its FrameSyncEngine in the `Awake()` method.

### `OnFrameSyncGameCreated`
Called after the FrameSyncAgent created its FrameSyncGame in the `Awake()` method.

### `OnCollectLocalPlayerInputs` 
Called every frame to collect the inputs of the local player.

[1]: https://www.socketweaver.com
[2]: https://www.socketweaver.com
[3]: https://www.socketweaver.com
[4]: https://www.socketweaver.com
[5]: https://www.socketweaver.com
[6]: https://www.socketweaver.com