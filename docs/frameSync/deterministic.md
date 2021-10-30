# **Deterministic**

You game logic must be deterministic to the bit-level. The FrameSync library only sends and manages players inputs. This means that given the same input, your game logic should produce the exact same game states on all supported platforms.

### **Challenages to Achieve Cross-platform Deterministic**
- **Floating point**: nearly impossible to have deterministic floating point calculation on different machines. 
- **Physics Engine**: Most physics engines use floating point so they are not deterministic on different machines.
- **Other Tools**: Similar to the physics engines, probably all the tools that you currently use (Navigation, Animatior, StateMachine, BehaviourTree, etc...) are not deterministic on different machines.

### **FixedMath**
FrameSync provides a fixed point math library [FixedMath][1] which is cross-platform deterministic. 

| **FixedMath**       | **Unity**                          |
| ----------- | ------------------------------------ |
| [FMath][1]       |  `Mathf`  |
| [FFloat][2]       |  `float`  |
| [FVector2][3]       |  `Vector2`  |
| [FVector3][4]       |  `Vector3`  |
| [FVector4][5]       |  `Vector4`  |
| [FMatrix4x4][6]       |  `Matrix4x4`  |
| [FQuaternion][7]       |  `Quaternion`  |
| [FTransform][8]       |  `Transform`  |

You can use it to replace `float`, `Vector2`, `Vector3`, `Quaternion`, `Matrix4x4`, `Mathf`, and the `Transform` component to implment your game logic.

### **FPhyscis**
Cross-platform deterministic 2D and 3D physics engines which run on the FixedMath library. They are designed to be used with the FrameSync library.

### **Deterministic Execution Order**
You can implement your game logic in the IFrameSync interfaces as their update order is guarenteed deterministic.


[1]: ../fixedmath/fixedmath.md
[2]: ../fixedmath/fmath.md
[3]: ../fixedmath/ffloat.md
[4]: ../fixedmath/fvector2.md
[5]: ../fixedmath/fvector3.md
[6]: ../fixedmath/fvector4.md
[7]: ../fixedmath/fmatrix4x4.md
[8]: ../fixedmath/fquaternion.md