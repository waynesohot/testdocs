# FMath.Deg2Rad

public static float Deg2Rad;

## Description

Degrees-to-radians conversion constant (Read Only).

This is equal to (PI * 2) / 360.

=== "C#"
    ``` c#
    using UnityEngine;
    using SocketWeaver.FixedMath;

    public class ExampleClass : MonoBehaviour
    {
        public FFloat deg = FFloat.FromDivision(30, 1);

        void Start()
        {
            FFloat rad = deg * FMath.Deg2Rad;
            Debug.Log(deg + " degrees are equal to " + rad + " radians.");
        }
    }
    ```