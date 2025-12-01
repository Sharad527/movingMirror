# movingMirror
The neural operator we are going to build to solve this problem focusses on is different. Here there are two aspects of this neural network which makes it different from the rest
+ Matrix valued output of the network
+ Complex entries of the output along with weights, biases and activation function

  We wish to leverage these two facts to obtain the $\beta_{\omega k}$ function. The expression for $\beta_{\omega k}$ is given as
  
```math
  \beta_{\omega k}=\int_{-\infty}^{+\infty} dV \frac{e^{i(U_{cl}(V)k-V\omega)}}{\sqrt{4\pi|\omega|}\sqrt{4\pi |k|}}(-k\partial_V U_{cl}(V)-\omega)
```

The bottleneck lies in the above expression. The $U_{cl}$ is very difficult to obtain in a general context. Also, the integral has infinite limits. The standard method to calculate the integration involves various approximation procedures that introduces a lot of error. In this work, we will approximate the $\beta$ coefficient by a neural network which will completely by-pass the above integral. **One of the merits of this approach is that once the neural network is trained, one can obtain the $\beta$ coefficient of "nearby" trajectories instantly without doing the above computation explicitly.**

There are two frequencies that parameterise the coefficient. The coefficient itself tells us about how much of $\omega$, from past null infinity, is present in $k$. We wish to discretise these frequencies such that the $\beta$ becomes a rank 2 matrix with rows and columns indexed by the two frequencies. Henceforth, we will refer to it as the $\beta$ matrix. Since we wish to get a matrix valued output, the hidden layers are now also matrix valued instead of just an array. To that end, a single layer is then given as, 

```math
y^{(\mu+1)}_{ab} = \sigma(\sum_{c,d}W^{(\mu)}_{abcd}y^{(\mu)}_{cd}+b_{cd}^{(\mu)}).
```

In this problem, since the trajectories we consider are smooth, the appropriate choice of activation function is $\tanh (x)$. Another justification for using this activation functions is that since we are interested in a regression type problem, instead of classification, we choose a function which is smooth.


Various solutions of the $\beta$ coefficient exist in the literature. The idea is to generate data from these analytical solutions and train the neural network on them. Since these coefficients are complex valued, the neural network is to be complex valued as well. Complex-valued neural networks have been studied in the literature[1](https://arxiv.org/pdf/2302.08286). The activation function in our case is chosen to be the simplest. We implement the activation function separately on the real and imaginary parts of a single neuron,

```math
  y^{(\mu+1)}_{ab} = \sigma(\mathcal{Re}(\sum_{c,d}W^{(\mu)}_{abcd}y^{(\mu)}_{cd}+b_{cd}^{(\mu)})) + \sigma(\mathcal{Im}(\sum_{c,d}W^{(\mu)}_{abcd}y^{(\mu)}_{cd}+b_{cd}^{(\mu)})).
```



