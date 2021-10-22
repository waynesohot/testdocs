# **Input Settings**

InputSettings declare the inputs that your game uses. 

The `FrameSyncEngine` uses InputSettings to create player Input frames

## **Creating an InputSettings asset**

To create an InputSettings for your game, right click in the project browser, and select `Create->SocketWeaver->FrameSync->InputSettings`.

![img](./../../assets/framesync/CreateInputSettings.png){: width=1080 }

## **Editing Inputs**

![img](./../../assets/framesync/InputSettings.png){: width=512 }

- To add a new input, select the `+` icon of the `Inputs` list.
- To remove an input, select the input and select the `-` icon of the `Inputs` list.
- The name of an input must be unique. You cannot have two or more inputs with the same name.
- FrameSync supports inputs of type: `Trigger`, `Bool`, `Int`, `Float`, `Vector2`, and `Vector3`.
- Make sure to optimize the input data size by adjusting the input's min, max, and resolution.

## **Saving and Code Generation**

???+ caution

    Make sure that you entered the correct namespace of your project. Extension methods will be generated under the provided namespace to help you get and set the inputs.

To save your changes to the InputSettings, click on the `Save` button at the bottom of the Inspector.

## **Generated Extension Methods**

The generated extension methods are located at `Assets->SocketWeaver->framesync_generated_input->{Your namespace}`

![img](./../../assets/framesync/InputSettingsLocation.png){: width=1080 }

=== "C#"
    ``` c#
        // Generated file, do not modify

        using SocketWeaver.FrameSync;
        using SocketWeaver.FixedMath;
        namespace SWExample.Pong
        {
            public static class gen_FrameSyncInputSettings
            {
                public static void SetInputY(this FrameSyncPlayer player, FFloat value)
                {
                    player.SetFloat(0, value);
                }
                public static FFloat GetInputY(this FrameSyncPlayer player)
                {
                    return player.GetFloat(0);
                }
            }
        }
    ```
