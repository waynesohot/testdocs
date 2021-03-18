## Description
A standard 4x4 transformation matrix.

| **Static Properties**  | **Description**  |  **Matrix4x4**     |  **FMatrix4x4**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| identity	| Returns the identity matrix (Read Only).| :material-check: |:material-check: |
| zero	| Returns a matrix with all elements set to zero (Read Only).| :material-check: |:material-check: |

| **Properties**  | **Description**  |  **Matrix4x4**     |  **FMatrix4x4**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| decomposeProjection	| This property takes a projection matrix and returns the six plane coordinates that define a projection frustum.
| determinant	| The determinant of the matrix. (Read Only)| :material-check: |:material-check: |
| inverse	| The inverse of this matrix. (Read Only)| :material-check: |:material-check: |
| isIdentity	| Checks whether this is an identity matrix. (Read Only)| :material-check: |:material-check: |
| lossyScale	| Attempts to get a scale value from the matrix. (Read Only)| :material-check: |:material-check: |
| rotation	| Attempts to get a rotation quaternion from this matrix.| :material-check: |:material-check: |
| this[int,int]	| Access element at [row, column].| :material-check: |:material-check: |
| transpose	| Returns the transpose of this matrix (Read Only).| :material-check: |:material-check: |

| **Public Methods**  | **Description**  |  **Matrix4x4**     |  **FMatrix4x4**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| GetColumn	| Get a column of the matrix.| :material-check: |:material-check: |
| GetRow	| Returns a row of the matrix.| :material-check: |:material-check: |
| MultiplyPoint	| Transforms a position by this matrix (generic).| :material-check: |:material-check: |
| MultiplyPoint3x4	| Transforms a position by this matrix (fast).| :material-check: |:material-check: |
| MultiplyVector	| Transforms a direction by this matrix.| :material-check: |:material-check: |
| SetColumn	| Sets a column of the matrix.| :material-check: |:material-check: |
| SetRow	| Sets a row of the matrix.| :material-check: |:material-check: |
| SetTRS	| Sets this matrix to a translation, rotation and scaling matrix.| :material-check: |:material-check: |
| ToString	| Returns a formatted string for this matrix.| :material-check: |:material-check: |
| TransformPlane	| Returns a plane that is transformed in space.| :material-check: |:material-check: |
| ValidTRS	| Checks if this matrix is a valid transform matrix.| :material-check: |:material-check: |

| **Static Methods**  | **Description**  |  **Matrix4x4**     |  **FMatrix4x4**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Frustum	| This function returns a projection matrix with viewing frustum that has a near plane defined by the coordinates that were passed in.
| Inverse3DAffine	| Computes the inverse of a 3D affine matrix.| :material-check: |:material-check: |
| LookAt	| Create a "look at" matrix.| :material-check: |:material-check: |
| Ortho	| Create an orthogonal projection matrix.| :material-check: |:material-check: |
| Perspective	| Create a perspective projection matrix.| :material-check: |:material-check: |
| Rotate	| Creates a rotation matrix.| :material-check: |:material-check: |
| Scale	| Creates a scaling matrix.| :material-check: |:material-check: |
| Translate	| Creates a translation matrix.| :material-check: |:material-check: |
| TRS	| Creates a translation, rotation and scaling matrix.| :material-check: |:material-check: |

| **Operators**  | **Description**  |  **Matrix4x4**     |  **FMatrix4x4**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| operator *	| Multiplies two matrices.| :material-check: |:material-check: |