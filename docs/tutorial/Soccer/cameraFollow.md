# **Camera**

Currently, the camera does not follow the car when the car moves. In this section, we will create a simple script to make the camera follows the car.

- Create a new script `SoccerCameraFollow` in the `Soccer` folder.
- Attach the `SoccerCameraFollow` script to the `Main Camera`.

Replace the contents of the script with the following:

=== "C#"
    ``` c#
    using SocketWeaver.FPhysics3D;
    using UnityEngine;

    namespace SWExample.Soccer
    {
        public float distance = 7f;
        public float height = 2f;
        public float rotationDamping = 2.0f;

        public Transform _car;

        public class SoccerCameraFollow : MonoBehaviour
        {
            void LateUpdate()
            {
                if (_car != null)
                {
                    Quaternion newRotation = Quaternion.Slerp(transform.rotation, _car.rotation, rotationDamping * Time.deltaTime);

                    Vector3 newPosition = _car.position - newRotation * Vector3.forward * distance;
                    newPosition.y = _car.position.y + height;

                    transform.position = newPosition;
                    transform.LookAt(_car);
                }
            }
        }
    }

    ```