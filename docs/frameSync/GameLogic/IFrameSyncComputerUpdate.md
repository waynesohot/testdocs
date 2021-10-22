# **IFrameSyncComputerUpdate**

## Declaration
=== "C#"
    ``` c#
    public interface IFrameSyncComputerUpdate
    {
        void OnComputerUpdate(FrameSyncUpdateType frameSyncUpdateType);
    }
    ```

## **Parameters**

| **Name**       |                         |
| ----------- | ------------------------------------ |
| frameSyncUpdateType     |  The update type.  |

## **Description**

Called by the FrameSyncEngine to update the computer owned `FrameSyncBehaviour` during frame simulation.

## **Example**
=== "C#"
    ``` c#
    public class ComputerMovement : MonoBehaviour, IFrameSyncComputerUpdate
    {
        public FFloat speed = FFloat.FromDivision(5, 1);

        public FTransform fTransform;

        public void OnComputerUpdate(FrameSyncUpdateType frameSyncUpdateType)
        {
            FFloat diretion = FFloat.zero;

            if (fTransform.position.y > FFloat.FromDivision(10, 1))
            {
                diretion = -FFloat.one;
            }
            else if (fTransform.position.y < -FFloat.FromDivision(10, 1))
            {
                diretion = FFloat.one;
            }

            FVector3 displacement = speed * FrameSyncTime.fixedDeltaTime * new FVector3(FFloat.zero, diretion, FFloat.zero);
            fTransform.position += displacement;
        }
    }
    ```