---
layout: post
title: Softmax function
key: 20201118
tags:
  - Python
  - deep learning
  - deep neural networks
---

## Softmax Function

1. Raise e(the mathematical constant) to the power of each those numbers
2. Sum up all the exponentails. This result is the denominator.
3. Use each number's exponential as its numerator.
4. calculate numerator / denominator

![equation](https://raw.githubusercontent.com/hadleyhzy34/deep-learning/main/deep_neural_network/source/softmax_functions.png)

<!--more-->

```python
import numpy as np

def softmax(xs):
    return np.exp(xs)/sum(np.exp(xs))

xs = np.array([-1,0,3,5])
print(softmax(xs))
```

    [0.002 0.006 0.118 0.874]



```python
test = np.array([-4,2,5])
print(softmax(test))
test1 = np.array([-5,-4,-3,-2,-1,4])
np.set_printoptions(formatter={'float': '{: 0.8f}'.format})
print(softmax(test1))
```

    [ 0.00011754  0.04742030  0.95246216]
    [ 0.00012212  0.00033195  0.00090233  0.00245278  0.00666736  0.98952347]









