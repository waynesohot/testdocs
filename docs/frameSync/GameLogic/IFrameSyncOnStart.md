# **IFrameSyncStart**

## Declaration
=== "C#"
    ``` c#
    public interface IFrameSyncStart
    {
        void OnStart(FrameSyncBehaviour frameSyncBehaviour);
    }
    ```

## **Parameters**

| **Name**       |                         |
| ----------- | ------------------------------------ |
| frameSyncBehaviour     |  The `FrameSyncBehaviour` component attached to the GameObject.  |

## **Description**

Called before the first IFrameSyncPlayerUpdate and IFrameSyncComputerUpdate. Implement this interface to initialzie the component.

## **Example**
=== "C#"
    ``` c#
    public class MyGameManager : MonoBehaviour, IFrameSyncStart
    {
        FFloat[] values;

        public void OnStart(FrameSyncBehaviour frameSyncBehaviour)
        {
            values = new FFloat[10];
        }
    }
    ```