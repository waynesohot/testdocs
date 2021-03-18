## Description
Representation of 3D vectors and points.

| **Static Properties**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| back	| Shorthand for writing Vector3(0, 0, -1).| :material-check: |:material-check: |
| down	| Shorthand for writing Vector3(0, -1, 0).| :material-check: |:material-check: |
| forward	| Shorthand for writing Vector3(0, 0, 1).| :material-check: |:material-check: |
| left	| Shorthand for writing Vector3(-1, 0, 0).| :material-check: |:material-check: |
| negativeInfinity	| Shorthand for writing Vector3(float.NegativeInfinity, float.NegativeInfinity, float.NegativeInfinity).| :material-check: |:material-close: |
| one	| Shorthand for writing Vector3(1, 1, 1).| :material-check: |:material-check: |
| positiveInfinity	| Shorthand for writing Vector3(float.PositiveInfinity, float.PositiveInfinity, float.PositiveInfinity).| :material-check: |:material-close: |
| right	| Shorthand for writing Vector3(1, 0, 0).| :material-check: |:material-check: |
| up	| Shorthand for writing Vector3(0, 1, 0).| :material-check: |:material-check: |
| zero	| Shorthand for writing Vector3(0, 0, 0).| :material-check: |:material-check: |

| **Properties**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| magnitude	| Returns the length of this vector (Read Only).| :material-check: |:material-check: |
| normalized	| Returns this vector with a magnitude of 1 (Read Only).| :material-check: |:material-check: |
| sqrMagnitude	| Returns the squared length of this vector (Read Only).| :material-check: |:material-check: |
| this[int]	| Access the x, y, z component using [0], [1], [2] respectively.| :material-check: |:material-check: |
| x	| X component of the vector.| :material-check: |:material-check: |
| y	| Y component of the vector.| :material-check: |:material-check: |
| z | Z component of the vector.| :material-check: |:material-check: |

| **Constructors**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Vector3	| Constructs a new vector with given x, y, z components.| :material-check: |:material-close: |
| FVector3	| Constructs a new vector with given x, y, z components.| :material-close: |:material-check: |

| **Public Methods**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Equals	| Returns true if the given vector is exactly equal to this vector.| :material-check: |:material-check: |
| Normalize	| Makes this vector have a magnitude of 1.| :material-check: |:material-check: |
| Set	| Set x, y, z components of an existing Vector3.| :material-check: |:material-check: |
| ToString	| Returns a formatted string for this vector.| :material-check: |:material-check: |

| **Static Methods**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Angle	| Returns the unsigned angle in degrees between from and to.| :material-check: |:material-check: |
| ClampMagnitude	| Returns a copy of vector with its magnitude clamped to maxLength.| :material-check: |:material-check: |
| Cross	| Cross Product of two vectors. | :material-check: |:material-check: |
| Distance	| Returns the distance between a and b.| :material-check: |:material-check: |
| Dot	| Dot Product of two vectors.| :material-check: |:material-check: |
| Lerp	| Linearly interpolates between vectors a and b by t.| :material-check: |:material-check: |
| LerpUnclamped	| Linearly interpolates between vectors a and b by t.| :material-check: |:material-check: |
| Max	| Returns a vector that is made from the largest components of two vectors.| :material-check: |:material-check: |
| Min	| Returns a vector that is made from the smallest components of two vectors.| :material-check: |:material-check: |
| MoveTowards	| Moves a point current towards target.| :material-check: |:material-check: |
| Normalize	| Makes this vector have a magnitude of 1.| :material-check: |:material-check: |
| OrthoNormalize	| Makes vectors normalized and orthogonal to each other.| :material-check: |:material-check: |
| Project	| Projects a vector onto another vector.| :material-check: |:material-check: |
| ProjectOnPlane	| Projects a vector onto a plane defined by a normal orthogonal to the plane.| :material-check: |:material-check: |
| Reflect	| Reflects a vector off the vector defined by a normal.| :material-check: |:material-check: |
| RotateTowards	| Rotates a vector current towards target.| :material-check: |:material-check: |
| Scale	| Multiplies two vectors component-wise.| :material-check: |:material-check: |
| SignedAngle	| Returns the signed angle in degrees between from and to.| :material-check: |:material-check: |
| Slerp	| Spherically interpolates between two vectors.| :material-check: |:material-check: |
| SlerpUnclamped	| Spherically interpolates between two vectors.| :material-check: |:material-check: |
| SmoothDamp	| Gradually changes a vector towards a desired goal over time.| :material-check: |:material-check: |

| **Operators**  | **Description**  |  **Vector3**     |  **FVector3**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| operator -	| Subtracts one vector from another.| :material-check: |:material-check: |
| operator *	| Multiplies a vector by a number.| :material-check: |:material-check: |
| operator /	| Divides a vector by a number.| :material-check: |:material-check: |
| operator +	| Adds two vectors.| :material-check: |:material-check: |
| operator ==	| Returns true if two vectors are approximately equal.| :material-check: |:material-check: |
| Vector3	| Converts(explicit) a FVector3 to a Vector3.| :material-close: |:material-check: |
| FVector3	| Converts(explicit) a Vector3 to a FVector3.| :material-close: |:material-check: |
| FVector3	| Converts(explicit) a FVector2 to a FVector3.| :material-close: |:material-check: |