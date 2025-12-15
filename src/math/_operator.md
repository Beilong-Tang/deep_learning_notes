# Vector operators

Here, I share some of the notations that might confuse people. See [here](https://en.wikipedia.org/wiki/Vector_operator) for details.

\\[
\nabla \rightarrow \text{gradient}
\\]
\\[
\nabla \cdot  \rightarrow \text{div} 
\\]
\\[
\Delta = \nabla \cdot \nabla  \rightarrow \text{Laplacian}
\\]
\\[
\nabla^2 = \nabla \nabla \rightarrow \text{Hessian}
\\]

- In \\(R^3\\), a vector field \\(F = F_x i + F_x j + F_x z\\), then \\(\nabla \cdot F = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}\\)

- For \\(f:R^n \rightarrow R\\), then  \\(\Delta f = \nabla \cdot \nabla f = \sum_{i=1}^n \frac{\partial^2 f}{\partial x_i^2} = tr(\nabla^2 f)\\)
    - For example, assume \\(f(x,y) = x^2 + y^2\\), then 
    \\[\nabla f = (2x, 2y)^T\\], and 
    \\[\nabla^2 f = \begin{bmatrix} 2 & 0  \\\\ 0 & 2 \end{bmatrix}\\], hence 
    \\[\Delta f = 2 + 2 = 4\\]

