# **IFrameSyncPlayerUpdate**

## Declaration
=== "C#"
    ``` c#
    public interface IFrameSyncPlayerUpdate
    {
        void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncUpdateType frameSyncUpdateType);
    }
    ```

## **Parameters**

| **Name**       |                         |
| ----------- | ------------------------------------ |
| player     |  The owner of the `FrameSyncBehaviour`.  |
| frameSyncUpdateType     |  The update type.  |

## **Description**

Called by the FrameSyncEngine to update the player owned `FrameSyncBehaviour` during frame simulation.

## **Example**
=== "C#"
    ``` c#
    public class PlayerMovement : MonoBehaviour, IFrameSyncPlayerUpdate
    {
        public FFloat speed = FFloat.FromDivision(5, 1);

        public FTransform fTransform;

        public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncUpdateType frameSyncUpdateType)
        {
            FFloat y = player.GetInputY();
            FVector3 displacement = speed * FrameSyncTime.fixedDeltaTime * new FVector3(FFloat.zero, y, FFloat.zero);
            fTransform.position += displacement;
        }
    }
    ```