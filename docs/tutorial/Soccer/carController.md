# **Call Controller**

The `VehicleController` script that attached to the `Car` uses the `MonoBehaviour` `Update()` to read player inputs and uses `FixedUpdate()` to simulate the vehicle physics. In this section, you will create a vehicle controller script that reads networked inputs and simulate the vehicle physics in a frame simulation update.

- Create a new script called `SoccerVehicleController` and attach it to the `Car`.
- Remove the existing `VehicleController` script.
- Add a `StaticFrameSyncBehaviour` compoennt to the `Car` and set `Own` to `Player1`.

Replace the contents in the `SoccerVehicleController` file with the following.

=== "C#"
    ``` c#
    using UnityEngine;
    using SocketWeaver.FrameSync;

    namespace SWExample.Soccer
    {
        //implements the IFrameSyncOnStart interface to get initialized by the FrameSyncEngine.
        //implements the IFrameSyncPlayerUpdate interface to get updated in a frame simulation. 
        public class SoccerVehicleController : MonoBehaviour, IFrameSyncOnStart, IFrameSyncPlayerUpdate
        {
            ArcadeCar car;

            CarInputData inputData;

            public void OnStart(FrameSyncBehaviour frameSyncBehaviour)
            {
                car = GetComponent<ArcadeCar>();
            }

            public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncGame game)
            {
                //read networked inputs
                inputData.steeringInput.y = player.GetInputY();
                inputData.steeringInput.x = player.GetInputX();

                car.inputData = inputData;

                //simulate car physics
                car.Simulate(FrameSyncTime.fixedDeltaTime);
            }
        }
    }
    ```