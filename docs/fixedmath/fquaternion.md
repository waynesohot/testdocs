## Description
Quaternions are used to represent rotations.

| **Static Properties**  | **Description**  |  **Quaternion**     |  **FQuaternion**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| identity	| The identity rotation (Read Only).| :material-check: |:material-check: |

| **Properties**  | **Description**  |  **Quaternion**     |  **FQuaternion**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| eulerAngles	| Returns or sets the euler angle representation of the rotation.| :material-check: |:material-check: |
| normalized	| Returns this quaternion with a magnitude of 1 (Read Only).| :material-check: |:material-check: |
| this[int]	| Access the x, y, z, w components using [0], [1], [2], [3] respectively.| :material-check: |:material-check: |
| w	| W component of the Quaternion. Do not directly modify quaternions.| :material-check: |:material-check: |
| x	| X component of the Quaternion. Don't modify this directly unless you know quaternions inside out.| :material-check: |:material-check: |
| y	| Y component of the Quaternion. Don't modify this directly unless you know quaternions inside out.| :material-check: |:material-check: |
| z	| Z component of the Quaternion. Don't modify this directly unless you know quaternions inside out.| :material-check: |:material-check: |

| **Constructors**  | **Description**  |  **Quaternion**     |  **FQuaternion**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Quaternion	| Constructs new Quaternion with given x,y,z,w components.| :material-check: |:material-close: |
| FQuaternion	| Constructs new Quaternion with given x,y,z,w components.| :material-close: |:material-check: |

| **Public Methods**  | **Description**  |  **Quaternion**     |  **FMaFQuaternionth**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Set	| Set x, y, z and w components of an existing Quaternion.| :material-check: |:material-check: |
| SetFromToRotation	| Creates a rotation which rotates from fromDirection to toDirection.| :material-check: |:material-check: |
| SetLookRotation	| Creates a rotation with the specified forward and upwards directions.| :material-check: |:material-check: |
| ToAngleAxis	| Converts a rotation to angle-axis representation (angles in degrees).| :material-check: |:material-check: |
| ToString	| Returns a formatted string of the Quaternion.| :material-check: |:material-check: |

| **Static Methods**  | **Description**  |  **Quaternion**     |  **FQuaternion**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Angle	| Returns the angle in degrees between two rotations a and b.| :material-check: |:material-check: |
| AngleAxis	| Creates a rotation which rotates angle degrees around axis.| :material-check: |:material-check: |
| Dot	| The dot product between two rotations.| :material-check: |:material-check: |
| Euler	| Returns a rotation that rotates z degrees around the z axis, x degrees around the x axis, and y degrees around the y axis; applied in that order.| :material-check: |:material-check: |
| FromToRotation	| Creates a rotation which rotates from fromDirection to toDirection.| :material-check: |:material-check: |
| Inverse	| Returns the Inverse of rotation.| :material-check: |:material-check: |
| Lerp	| Interpolates between a and b by t and normalizes the result afterwards. The parameter t is clamped to the range [0, 1].| :material-check: |:material-check: |
| LerpUnclamped	| Interpolates between a and b by t and normalizes the result afterwards. The parameter t is not clamped.| :material-check: |:material-check: |
| LookRotation	| Creates a rotation with the specified forward and upwards directions.| :material-check: |:material-check: |
| Normalize	| Converts this quaternion to one with the same orientation but with a magnitude of 1.| :material-check: |:material-check: |
| RotateTowards	| Rotates a rotation from towards to.| :material-check: |:material-check: |
| Slerp	| Spherically interpolates between quaternions a and b by ratio t. The parameter t is clamped to the range [0, 1].| :material-check: |:material-check: |
| SlerpUnclamped	| Spherically interpolates between a and b by t. The parameter t is not clamped.| :material-check: |:material-check: |

| **Operators**  | **Description**  |  **Quaternion**     |  **FQuaternion**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| operator *	| Combines rotations lhs and rhs.| :material-check: |:material-check: |
| operator ==	| Are two quaternions equal to each other?| :material-check: |:material-check: |