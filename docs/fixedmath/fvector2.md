## Description
Representation of 2D vectors and points.

| **Static Properties**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| down	| Shorthand for writing Vector2(0, -1).| :material-check: |:material-check: |
| left	| Shorthand for writing Vector2(-1, 0).| :material-check: |:material-check: |
| negativeInfinity	| Shorthand for writing Vector2(float.NegativeInfinity, float.NegativeInfinity).| :material-check: |:material-close: |
| one	| Shorthand for writing Vector2(1, 1).| :material-check: |:material-check: |
| positiveInfinity	| Shorthand for writing Vector2(float.PositiveInfinity, float.PositiveInfinity).| :material-check: |:material-close: |
| right	| Shorthand for writing Vector2(1, 0).| :material-check: |:material-check: |
| up	| Shorthand for writing Vector2(0, 1).| :material-check: |:material-check: |
| zero	| Shorthand for writing Vector2(0, 0).| :material-check: |:material-check: |


| **Properties**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| magnitude	| Returns the length of this vector (Read Only).| :material-check: |:material-check: |
| normalized	| Returns this vector with a magnitude of 1 (Read Only).| :material-check: |:material-check: |
| sqrMagnitude	| Returns the squared length of this vector (Read Only).| :material-check: |:material-check: |
| this[int]	| Access the x or y component using [0] or [1] respectively.| :material-check: |:material-check: |
| x	| X component of the vector.| :material-check: |:material-check: |
| y	| Y component of the vector.| :material-check: |:material-check: |

| **Constructors**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Vector2	| Constructs a new vector with given x, y components.| :material-check: |:material-close: |
| FVector2	| Constructs a new vector with given x, y components.| :material-close: |:material-check: |

| **Public Methods**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Equals	| Returns true if the given vector is exactly equal to this vector.| :material-check: |:material-check: |
| Normalize	| Makes this vector have a magnitude of 1.| :material-check: |:material-check: |
| Set	| Set x and y components of an existing Vector2.| :material-check: |:material-check: |
| ToString	| Returns a formatted string for this vector.| :material-check: |:material-check: |

| **Static Methods**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Angle	| Returns the unsigned angle in degrees between from and to.| :material-check: |:material-check: |
| ClampMagnitude	| Returns a copy of vector with its magnitude clamped to maxLength.| :material-check: |:material-check: |
| Distance	| Returns the distance between a and b.| :material-check: |:material-check: |
| Dot	| Dot Product of two vectors.| :material-check: |:material-check: |
| Lerp	| Linearly interpolates between vectors a and b by t.| :material-check: |:material-check: |
| LerpUnclamped	| Linearly interpolates between vectors a and b by t.| :material-check: |:material-check: |
| Max	| Returns a vector that is made from the largest components of two vectors.| :material-check: |:material-check: |
| Min	| Returns a vector that is made from the smallest components of two vectors.| :material-check: |:material-check: |
| MoveTowards	| Moves a point current towards target.| :material-check: |:material-check: |
| Perpendicular	| Returns the 2D vector perpendicular to this 2D vector. The result is always rotated 90-degrees in a counter-clockwise direction for a 2D coordinate system where the positive Y axis goes up.| :material-check: |:material-check: |
| Reflect	| Reflects a vector off the vector defined by a normal.| :material-check: |:material-check: |
| Scale	| Multiplies two vectors component-wise.| :material-check: |:material-check: |
| SignedAngle	| Returns the signed angle in degrees between from and to.| :material-check: |:material-check: |
| SmoothDamp	| Gradually changes a vector towards a desired goal over time.| :material-check: |:material-check: |

| **Operators**  | **Description**  |  **Vector2**     |  **FVector2**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| operator -	| Subtracts one vector from another.| :material-check: |:material-check: |
| operator *	| Multiplies a vector by a number.| :material-check: |:material-check: |
| operator /	| Divides a vector by a number.| :material-check: |:material-check: |
| operator +	| Adds two vectors.| :material-check: |:material-check: |
| operator ==	| Returns true if two vectors are approximately equal.| :material-check: |:material-check: |
| Vector2	| Converts a Vector3 to a Vector2.| :material-check: |:material-close: |
| Vector3	| Converts a Vector2 to a Vector3.| :material-check: |:material-close: |
| Vector2	| Converts(explicit) a FVector2 to a Vector2.| :material-close: |:material-check: |
| FVector2	| Converts(explicit) a FVector3 to a FVector2.| :material-close: |:material-check: |
| FVector2	| Converts(explicit) a Vector2 to a FVector2.| :material-close: |:material-check: |
| FVector2	| Converts(explicit) a Vector3 to a FVector2.| :material-close: |:material-check: |