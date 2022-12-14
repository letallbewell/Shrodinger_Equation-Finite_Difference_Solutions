# Finite Difference Approximation and the Schrodinger Equation

This repo demonstrates a simple algorithm using `NumPy` functions and the Finite Difference approximation that can solve the Schrodinger equation in any dimension under arbitrary potentials and boundary conditions.

## In 1 dimension        

The Schrodinger equation with the constants omitted is:

$$ \frac{d^2 \Psi}{dx^2} + x^2 \Psi = E \Psi $$

We will solve the problem on a discrete grid $x = [x_1,...,x_i,...,x_N]$ on the interval $[-L,L]$. The finite difference approximation of the second derivative is:

$$ \frac{d^2 \Psi}{dx^2} \left( x_i \right) = \frac{\Psi_{i-1} - 2 \Psi_i + \Psi_{i+1}}{h^2} + \mathcal{O} \left( h^2 \right), $$

where $h$ is the grid spacing.

The differential equation can now be converted into a matrix eigenvalue problem by finding the eigenvalues of the matrix $H =D2 + V$. $D2$ is created by rolling $[-2, 1, 0,...,0, 1]$ across the rows, and $V$ is the diagonal matrix constructed from the potential evaluated on the grid.

The numerical solutions start to diverge from the analytic solutions for higher quantum numbers because their oscillatory behavior will eventually break the resolution power of the grid. You can reduce $h$ or use a higher-order Finite Difference approximation to combat this. Decreasing $h$ too much is not desirable because the floating point approximation error will increase, but the Finite Difference approximation error will go down. We can always operate in a sweet spot for solving elementary problems. See [a seminar report](https://drive.google.com/file/d/1DIg4EB0zVfoEOu_4VoJFeTKqtzHaXho8/view?usp=sharing) I did in the past for a little bit more detail.

### Infinite Potential Well

![1d_IPW](https://user-images.githubusercontent.com/43025445/188310401-607b39a0-d84c-4fb6-b76f-04edfca4c2d7.png)

### Harmonic Potential Well

![1d_HPW](https://user-images.githubusercontent.com/43025445/188310414-035467a3-9443-4474-8df2-6d823ed7e5c2.png)

## Extension to higher dimensions

The method easily extends to higher dimensions through tensor product operation. For example, in 3D, $\nabla^2$ can be approximated using the same $D2$ matrix as

$$ D2 \otimes I_{N \times N} \otimes I_{N \times N} + I_{N \times N} \otimes D2 \otimes I_{N \times N} + I_{N \times N} \otimes I_{N \times N} \otimes D2 $$

### 2d Harmonic Potential Well
![](https://user-images.githubusercontent.com/43025445/188310465-ba027fe0-04a9-46aa-ad12-2efc7b06a102.png)

### 3d Hydrogen Atom Potential

The following plot is a cross-section of the wave functions (I thought a 3d density plot is not worth the trouble). The slider inside the jupyter notebook changes the cross-section plane.

![Screen Shot 2022-09-04 at 4 45 59 PM](https://user-images.githubusercontent.com/43025445/188310541-26432a58-e740-4697-a1c5-f798b424ed1b.png)

