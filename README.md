# movingMirror
The neural operator we are going to build to solve this problem focusses on is different. Here there are two aspects of this neural network which makes it different from the rest
+ Matrix valued output of the network
+ Complex entries of the output along with weights, biases and activation function

  We wish to leverage these two facts to obtain the $\beta_{\omega k}$ function. The expression for $\beta_{\omega k}$ is given as
  
  ```math
  \beta_{\omega k}=\int_{-\infty}^{+\infty} dV \frac{e^{i(U_{cl}(V)k-V\omega)}}{\sqrt{4\pi|\omega|}\sqrt{4\pi |k|}}(-k\dl_V U_{cl}(V)-\omega)
  ```math

The bottleneck lies in the above expression. The $U_{cl}$ is very difficult to obtain in a general context. Also, the integral has infinite limits. The standard method to calculate the integration involves various approximation procedures that introduces a lot of error. In this work, we will approximate the $\beta$ coefficient by a neural network which will completely by-pass the above integral. 

Various solutions of $\beta$ coefficient exists in the literature. The idea is to generate data from these analytical solutions and train the neural network on them. Since these coefficients are complex valued, the neural network is to be complex valued as well. There are two frequecies that parameterise the coefficient. The coefficient itself tells us about how much of $\omega$ from the past null infinity is present in $k$. 

  Write about how the network is matrix valued. include equations. also mention equations and why it is matrix valued
  write about the complex numbers and why it is required. show the implementation of complex activation function.

  Also make sure to add what are the pitfalls of the above.
