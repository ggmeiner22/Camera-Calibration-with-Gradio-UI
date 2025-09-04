## Camera Model Basics

#### Write the pinhole camera model in matrix form
$$
\begin{gathered}
\lambda
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
= 
\begin{bmatrix}
f_x & \gamma & c_x & 0 \\
0 & f_y & c_y & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
\omega_{11} & \omega_{12} & \omega_{13} & \tau_x \\
\omega_{21} & \omega_{22} & \omega_{23} & \tau_y \\
\omega_{31} & \omega_{32} & \omega_{33} & \tau_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u \\ v \\ w \\ 1
\end{bmatrix}
\end{gathered}
$$
#### Derive the basic perspective projection equation when the frame is aligned with the world frame (i.e., no rotation or translation)

$$
\begin{gathered}
\lambda
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
= 
\begin{bmatrix}
f_x & 0 & c_x & 0 \\
0 & f_y & c_y & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
\omega_{11} & \omega_{12} & \omega_{13} & \tau_x \\
\omega_{21} & \omega_{22} & \omega_{23} & \tau_y \\
\omega_{31} & \omega_{32} & \omega_{33} & \tau_z \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u \\ v \\ w \\ 1
\end{bmatrix}
\\\\
\Rightarrow~~
\lambda
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
= 
\begin{bmatrix}
f_x & 0 & c_x & 0 \\
0 & f_y & c_y & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u \\ v \\ w \\ 1
\end{bmatrix}
\\\\
\Rightarrow~~
\lambda
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
= 
\begin{bmatrix}
f_x & 0 & c_x & 0 \\
0 & f_y & c_y & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
u \\ v \\ w \\ 1
\end{bmatrix}
\\\\
\Rightarrow~~
\lambda
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
= 
\begin{bmatrix}
f_x & 0 & c_x \\
0 & f_y & c_y \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u \\ v \\ w
\end{bmatrix}
\\\\
\Rightarrow~~
\lambda = w, ~~~x = \frac{f_xu}{w} + c_x, ~~~y = \frac{f_yv}{w} + c_y
\end{gathered}
$$

#### Where is the camera center represented in the pinhole model matrix?

The camera's center is represented by the column vector $\begin{bmatrix}c_x\\c_y\end{bmatrix}$ contained within the intrinsic parameter matrix.
#### Why is the pinhole camera model $\textemdash$ originally nonlinear $\textemdash$ expressed in matrix form?

The pinhole camera model is a nonlinear model when you restrict yourself to the standard Cartesian coordinates, because of the division by $z$ required. However, by extending the model into homogenous coordinates, the pinhole camera model can be rewritten as a linear transformation into an augmented projected space, preserving the computational efficiency of the model while also allowing for an easy conversion back into the non-linear Cartesian projected space.
#### How is it even possible to represent the pinhole camera model as a matrix if it is originally nonlinear?

See above. By representing the pinhole camera model in using homogeneous coordinates, the result can be represented as a product as a scalar $\lambda$ and a vector. This preserves the linear nature of the model on the right, while allowing for the easy derivation of the desired part of the result (dividing by $\lambda$)
## Intrinsic Parameters
#### Explain the role of the focal length in the pinhole model

The purpose of the focal length is to determine the scale of objects in the projected space. A larger focal length means objects will appear larger (i.e. "zoomed in", smaller field of view), while a smaller focal length means objects will appear smaller (i.e. "zoomed out", larger field of view)
#### What geometric distortions are the result of changing the focal length?

See above. By changing the focal length, you are changing the size of objects in the projected space, which can have several side effects. The most obvious of these is that the field of view will get smaller or larger, and objects will appear larger or smaller, but additionally, a higher focal length will minimize differences in depth, while a lower focal length will exaggerate these differences.
#### Why do we have two focal length values, $f_x$ and $f_y$?

Having separate focal length values for the $x$ and $y$ dimensions individually allows you to account for scenarios where the camera sensor pixels are not perfectly square.
#### Define the principal point ($c_x$, $c_y$) and explain why it is needed.

The principal point ($c_x$, $c_y$) represents the point where the optical axis (i.e. the $z$ axis, or the axis that runs perpendicular to the projected space) intersects with this projected space. This point is needed because the camera is not generally at this point, so including the principal point allows one to ensure that the world space is correctly projected onto the camera space.
## Extrinsic Parameters
#### What is the value of the rotation matrix when there is no rotation?
$$
\begin{gathered}
\Omega = \begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
\end{gathered}
$$
#### What is the value of the translation vector when there is no translation?
$$
\begin{gathered}
\tau = \begin{bmatrix}
0 \\ 0 \\ 0
\end{bmatrix}
\end{gathered}
$$
#### Why do we use the inverse of the extrinsic matrix when plotting cameras with respect to the world frame?

The extrinsic matrix can be thought of as representing the rotation and translation of your world space. Hence, applying the extrinsic matrix to your world coordinates, like:
$$
\mathbf{x}_{\text{world}} =
\begin{bmatrix}
\Omega & \tau
\end{bmatrix}
\mathbf{x}_{\text{camera}},~~ \text{or} ~~
\mathbf{x}_{\text{world}} =
\Omega \mathbf{x}_{\text{camera}} + \tau\
$$

To do the inverse, and solve for the camera coordinates with respect to the world, we get:

$$
\mathbf{x}_{\text{camera}} =
\Omega^{-1}(\mathbf{x}_{\text{world}}  - \tau)
,~~ \text{or} ~~
\mathbf{x}_{\text{camera}} =
\begin{bmatrix}
\Omega^{-1} & -\tau\Omega^{-1}
\end{bmatrix}
\mathbf{x}_{\text{world}}

$$
Just keep in mind that, since $\Omega$ is orthogonal, $\Omega^{-1} = \Omega^T$
#### Why is the inverse of the rotation matrix its transpose?

$\Omega$ is orthogonal, therefore $\Omega^{-1} = \Omega^T$

#### When factorizing the rotation matrix using SVD, what do we expect to obtain in the diagonal matrix? Why?

When performing a SVD decomposition on the rotation matrix, the resultant diagonal matrix from the factorization is expected to be the identity matrix, as any other matrix would imply that the rotation matrix is not a pure rotation, but rather a mixture of rotation, scaling, and shearing.

### If we are given an estimated rotation matrix obtained as the output of some numerical procedure, what steps do we usually perform using the SVD to ensure the rotation matrix is correct?

 We take the rotation matrix and perform an SVD decomposition, then look at the middle term of the decomposition, which is a diagonal matrix $\Sigma$. If $\Sigma$ is the identify matrix, then our original rotation matrix was correct. Otherwise, we can replace the value of $\Sigma$ in the SVD decomposition with an identity matrix, and remultiply out the factors of the decomposition to obtain a corrected rotation matrix, without any distortions from scaling or shearing.

#### The columns of the rotation matrix can be considered as 3D vectors. What to the columns of a rotation matrix represent?

The three column vectors in the rotation matrix represent the $x$, $y$, and $z$ axes of the camera, relative to the world's coordinate space, forming an orthogonal basis.

## Lens Distortion

### What is lens distortion and how is it modeled mathematically?

Lens distortion is any deviation from the ideal pinhole camera model that is produced by real world lenses. The most common of these distortions, *radial distortion*, can be modeled mathematically in the following manner:
$$
\begin{gathered}
x'=x(1+\beta_1 r^2 + \beta_2 r^4)
\\\\
y'=y(1+\beta_1 r^2 + \beta_2 r^4)
\end{gathered}
$$
where $(x, y)$ is the original image positions, $(x',y')$ are the final image positions. parameters $\beta_1$ and $\beta_2$ control the degree of the distortion.

## Homography Transformation

#### How is the geometry of the homography different from the standard perspective projection of 3D objects?

While the standard perspective projection is concerned with mapping 3D points in the world to 2D points in the image plane, the homography transform is concerned with mapping 2D points on one plane (presumably outside of the image plane) onto the image plane. That is, a homography transform does not concern itself with variable $z$ coordinates in the projected object; the $z$ coordinate itself is assumed to be $0$.

#### Why do we usually only need 4 points to estimate the homography transformation?
 
The homography transformation matrix has 9 unknowns, and therefore 8 degrees of freedom. Therefore, a system of 8 equations is required to ensure the values in the homography transformation matrix. Each input point to the transformation equation results in two linear equations for the projected $x$ and $y$ coordinates. Therefore, 4 unique points will generated the 8 necessary equations in order to determine the unknowns in the homography transformation matrix.
#### Given a homography matrix, what does this matrix have in terms of geometric transformations from the pinhole camera.

The homography matrix can consist of a combination of rotation, translation, scaling, and shearing (in essence, any possible linear transformation) that projects a plane in 3D space onto the image plane.

#### How do we recover the full rotation matrix from the homography transformation?

We can consider the homography transformation matrix $H$ to be a simplified product of the intrinsic and extrinsic parameter matrices from the pinhole camera model.
$$
\begin{gathered}
\lambda
\begin{bmatrix}
u \\ v \\ 1
\end{bmatrix}
= K \begin{bmatrix}
\omega_{11} & \omega_{12} & \omega_{13} & \tau_x \\
\omega_{21} & \omega_{22} & \omega_{23} & \tau_y \\
\omega_{31} & \omega_{32} & \omega_{33} & \tau_z 
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ 0 \\ 1
\end{bmatrix}

\\\\
\text{which can be simplified to...}
\\\\
\lambda
\begin{bmatrix}
u \\ v \\ 1
\end{bmatrix} =
K \begin{bmatrix}
\omega_{11} & \omega_{12} & \tau_x \\
\omega_{21} & \omega_{22} & \tau_y \\
\omega_{31} & \omega_{32} & \tau_z 
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
\\\\
\Rightarrow
\lambda
\begin{bmatrix}
u \\ v \\ 1
\end{bmatrix} =
H
\begin{bmatrix}
x \\ y \\ 1
\end{bmatrix}
, H = K \begin{bmatrix} R & t\end{bmatrix} = K \begin{bmatrix} r_1 & r_2 & t\end{bmatrix}
\end{gathered}
$$

You can then extract just the relevant extrinsic parameters by multiplying by $K^{-1}$, then extracting and normalizing $r_1$ and $r_2$ by divided by their magnitude, $\lambda$ (which should be shared between the two vectors). $r_3$ and then be computed through $r_1 \times r_2$, and the translation vector should be divided by the same $\lambda$ before converting to the final extrinsic parameter matrix.
#### How do we remove the effect of the scaling factor that is mixed in the elements of the homography transformation?

See above. Normalizing the $r_1$ and $r_2$ from the homography by dividing by some $\lambda$, which should be the shared magnitude of $r_1$ and $r_2$, which can then also be used to correct for the scaling of the translation vector by dividing $t$ by $\lambda$.
