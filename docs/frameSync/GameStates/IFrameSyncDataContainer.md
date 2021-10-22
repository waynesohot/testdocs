# **IFrameSyncDataContainer**

## Declaration
=== "C#"
    ``` c#
    public interface IFrameSyncDataContainer
    {
        void OnImport(SWBytes buffer);
        void OnExport(SWBytes buffer);
    }
    ```

## **Description**

Called by the FrameSyncEngine to export/import the data of the `FrameSyncBehaviour`. You should implement this interface in a `MonoBehaviour` component if it contains game states that needs to be restored for deterministic simulation.

## **Example**
=== "C#"
    ``` c#
    public class PlayerMovement : MonoBehaviour, IFrameSyncPlayerUpdate, IFrameSyncDataContainer
    {
        public FFloat speed = FFloat.FromDivision(5, 1);

        public FTransform fTransform;

        public void OnExport(SWBytes buffer)
        {
            buffer.Push(fTransform.position.y);
        }

        public void OnImport(SWBytes buffer)
        {
            FFloat y = buffer.PopFFloat();
            FVector3 pos = fTransform.position;
            fTransform.position = new FVector3(pos.x, y, pos.z);
        }

        public FrameSyncDebugItemGroup OnExportDebugInfo()
        {
            FrameSyncDebugItemGroup group = new FrameSyncDebugItemGroup();
            group.name = "PlayerMovement";
            group.Add("y", fTransform.position.y.ToString());
            return group;
        }

        public void OnPlayerUpdate(FrameSyncPlayer player, FrameSyncUpdateType frameSyncUpdateType)
        {
            FFloat y = player.GetInputY();
            FVector3 displacement = speed * FrameSyncTime.fixedDeltaTime * new FVector3(FFloat.zero, y, FFloat.zero);
            fTransform.position += displacement;
        }
    }
    ```