# Fisher-Rao information matrix on Gaussian


This gives the detailed proof for equation `7` in Paper __Geodesic Diffusion Models for Medical Image-to-Image Generation__.


__Lemma__: Assume the we have a multivariate gaussian distribution:

\\[
p(\mathbf{x}|\mathbf{\mu}, \sigma) = \frac{1}{(2\pi\sigma^2)^{\frac{n}{2}}}\exp(-\frac{1}{2\sigma^2}||\mathbf{x}-\mathbf{\mu}||^2)
\\]
where \\(\mathbf{x}, \mathbf{\mu} \in \mathbb{R}^n\\) and \\(\sigma \in \mathbb{R}\\). Then the fisher-rao information matrix \\(\mathbf{I}\_{\theta}\\) is given as 
\\[
\mathbf{I}\_\theta = \begin{bmatrix}
\frac{1}{\sigma^2}\pmb{I} & 0 \\\\
0 & \frac{2n}{\sigma^2}
\end{bmatrix}
\in \mathbb{R}^{(n+1)}\times\mathbb{R}^{(n+1)}
\\]
where \\(\theta = (\mathbf{\mu}, \sigma)^T\\)


__Proof__: To calculate this, one needs to go over the derivatives.

Firstly, we know that 
\\[
\mathbf{I}\_\theta = \mathbb{E}[(\nabla\_\theta\log p(x|\theta))\cdot(\nabla\_\theta\log p(x|\theta))^T]
\\] for any distribution \\(p(x|\theta)\\)

Firstly, we know 
\\[
\begin{align}
\log p(\mathbf{x}|\mathbf{\mu}, \sigma) &= -\frac{n}{2}\log (2\pi\sigma^2) + (-\frac{1}{2\sigma^2}||\mathbf{x}-\mathbf{\mu}||^2) \quad \text{, therefore }\\\\
\frac{\partial\log p(\mathbf{x}|\mathbf{\mu}, \sigma)}{\partial \mathbf{\mu}} &=  \frac{\mathbf{x}-\mathbf{\mu}}{\sigma^2} \quad \text{and} \\\\
\frac{\partial\log p(\mathbf{x}|\mathbf{\mu}, \sigma)}{\partial \sigma} &= -\frac{n}{\sigma} + \frac{||\mathbf{x}-\mathbf{\mu}||^2}{\sigma^3}
\end{align}
\\]

Therefore, 
\\[
\nabla\_\theta\log p(\mathbf{x}|\mathbf{\mu}, \sigma)\ = (\frac{\mathbf{x}-\mathbf{\mu}}{\sigma^2}, -\frac{n}{\sigma} + \frac{||\mathbf{x}-\mathbf{\mu}||^2}{\sigma^3})^T
\\]

Then, let \\(l= \log p(\mathbf{x}|\mathbf{\mu}, \sigma)\\)
\\[
\mathbf{I}\_\theta = \mathbb{E}(\begin{bmatrix}
 (\frac{\partial l}{\partial{\mu\_1}})^2 & \frac{\partial l}{\partial{\mu\_1}} \frac{\partial l}{\partial{\mu\_2}} & \dots 
& \frac{\partial l}{\partial{\mu\_1}} \frac{\partial l}{\partial{\mu\_n}} & \frac{\partial l}{\partial{\mu\_1}} \frac{\partial l}{\partial{\sigma}} \\\\
\vdots &  & \ddots \\\\ 
 (\frac{\partial l}{\partial{\mu\_n}})^2 & \frac{\partial l}{\partial{\mu\_n}} \frac{\partial l}{\partial{\mu\_2}} & \dots 
& \frac{\partial l}{\partial{\mu\_n}} \frac{\partial l}{\partial{\mu\_n}} & \frac{\partial l}{\partial{\mu\_n}} \frac{\partial l}{\partial{\sigma}} \\\\
 \frac{\partial l}{\partial{\sigma}} \frac{\partial l}{\partial{\mu\_1}} & \frac{\partial l}{\partial{\sigma}} \frac{\partial l}{\partial{\mu\_2}} & \dots 
& \frac{\partial l}{\partial{\sigma}} \frac{\partial l}{\partial{\mu_n}} & (\frac{\partial l}{\partial{\sigma}})^2 
\end{bmatrix}) \\\\
\\]

Then, we derive formulas for \\(\mathbb{E}[\frac{\partial l}{\partial \mu_i}\frac{\partial l}{\partial \mu_j}]\\):

When \\(i = j\\): 
\\[
\begin{align}
\mathbb{E}[\frac{\partial l}{\partial \mu_i}\frac{\partial l}{\partial \mu_j}] &=\mathbb{E}[(\frac{\partial l}{\partial \mu_i})^2] =  \mathbb{E}[\frac{(x_i-\mu_i)^2}{\sigma^4}] \\\\
&= \frac{\mathbb{E}[(x_i-\mu_i)^2]}{\sigma^4} = \frac{\sigma^2}{\sigma^4} = \frac{1}{\sigma^2}
\end{align}
\\]

When \\(i \ne j\\):
\\[
\begin{align}
\mathbb{E}[\frac{\partial l}{\partial \mu_i}\frac{\partial l}{\partial \mu_j}] &= \mathbb{E}[\frac{(x_i-\mu_i)(x_j-\mu_j)}{\sigma^4}] \\\\
&= [\frac{\mathbb{E}[(x_i-\mu_i)]\mathbb{E}[(x_j-\mu_j)]}{\sigma^4}] = \frac{0}{\sigma^4} = 0
\end{align}
\\]

Now, we need to derive formulas for \\(\mathbb{E}[\frac{\partial l }{\partial \mu_i} \frac{\partial l}{\partial \sigma}]\\) and \\(\mathbb{E}[(\frac{\partial l}{\partial \sigma})^2]\\), and then we 
are done.

\\[
\begin{align}
\mathbb{E}[\frac{\partial l }{\partial \mu_i} \frac{\partial l}{\partial \sigma}] = \mathbb{E}[(x-\mu_i)] * \mathbb{E}[\frac{\partial l}{\partial \sigma}] \cdot \frac{1}{\sigma^2} = 0
\end{align}
\\]

Before deriving \\(\mathbb{E}[(\frac{\partial l}{\partial \sigma})^2]\\), we need to know that if \\(x \sim N (\mu, \sigma^2)\\), then \\(\mathbb{E}[(x-\mu)^4] = 3\sigma^4\\). This is called the 
fourth central moments of a gaussian.

\\[
\begin{align}
\mathbb{E}[(\frac{\partial l}{\partial \sigma})^2] = \frac{2n}{\sigma^2}
\end{align}
\\] where the full derivation is given at [here](../assets/math/fisher_rao_information_sigma.pdf):
<!-- <iframe src="../assets/math/fisher_rao_information_sigma.pdf" width="100%" height="600px" -->
Therefore, we can conclude that 

\\[
\mathbf{I}\_\theta = \begin{bmatrix}
\frac{1}{\sigma^2}\pmb{I} & 0 \\\\
0 & \frac{2n}{\sigma^2}
\end{bmatrix}
\\]
