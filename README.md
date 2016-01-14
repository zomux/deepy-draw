[![Requirements Status](https://requires.io/github/uaca/deepy-draw/requirements.svg?branch=master)](https://requires.io/github/uaca/deepy-draw/requirements/?branch=master)
[![GPL3](https://img.shields.io/badge/license-GPL3-blue.svg)](https://github.com/uaca/deepy-draw/blob/master/LICENSE)

# Another implementation of DRAW with deepy framework

Paper: http://arxiv.org/pdf/1502.04623

### Note

Core components in the implementation are copied from https://github.com/jbornschein/draw, thanks for the great work of https://github.com/jbornschein.

### Tricky parts in the model

- Differential filter functions that can zoom in and zoom out an image to get a glimpse
- Q Sampler
 - Differential sampling function to get a sample from distributions

### What does the sampler do, an analysis from computation graph

- Prior distribution P_z
 - This distribution generates latent variables used in image generation
- mean and deviation transform networks
 - These two networks transform inputs to mean and deviation vectors to form a distribution Q(z|x)
 - The goal for training these two network is to make Q(z|x) close to prior P_z
  - KL(Q(z|x) || P_z) is to evaluate how close these two distributions are
- But if we sample a latent variable from Q(z|x), another goal is to restore the original input x from z
 - So this means the model try to map any input to a similar latent vector
 - but it has to maintain a tiny difference so as to decode it back to x
- Then if we sample from P_z, we are sampling from Q(z|x) which we don't know what the x is


### Experiment on MNIST

```bash
python mnist_training.py
```

### MNIST Animation (work in progress)

![](https://github.com/zomux/deepy-draw/raw/master/plots/mnist-animation.gif)
