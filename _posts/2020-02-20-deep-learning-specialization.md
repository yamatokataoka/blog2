---
layout: post
title: Deep Learning Specialization
---

In this post, I will explain bihind the scenes of each programming assignments so that you can understand more about deep learning.

In five courses, you will learn the foundations of Deep Learning, understand how to build neural networks, and learn how to lead successful machine learning projects.

You will master not only the theory, but also see how it is applied in industry.

# Neural Networks and Deep Learning

In this course, you will:
- Understand the major technology trends driving Deep Learning
- Build, train and apply fully connected deep neural networks
- Know how to implement efficient (vectorized) neural networks
- Understand the key parameters in a neural network's architecture

## Week 2

Key Concepts on Programming Assignments
- Work with iPython Notebooks
- Become familiar with Python and Numpy
- Implement the main steps of an ML algorithm, including making predictions, derivative computation, and gradient descent.
- Build a logistic regression model, structured as a shallow neural network
- Be able to implement vectorization across multiple training examples
- Implement computationally efficient, highly vectorized, versions of models.

### Python Basics with numpy

In this assignment you will:

- Learn how to use numpy.
- Implement some basic core deep learning functions such as the softmax, sigmoid, dsigmoid, etc...
- Learn how to handle data by normalizing inputs and reshaping images.
- Recognize the importance of vectorization.
- Understand how python broadcasting works.

##### sigmoid function, np.exp()

You will implement the sigmoid function using both `math.exp()` and `np.exp()` on your iPython Notebook.

The Python math Library provides us access to some common math functions and constants in Python.  
Reference: [math — Mathematical functions](https://docs.python.org/3/library/math.html)

Using math,

```
1 / (1 + math.exp(-x))
```

> `1 / (1 + math.exp(-x))` - Add parentheses on `1 + math.exp(-x)` to make evaluate it first.
> Reference: [2.9. Order of Operations](https://runestone.academy/runestone/books/published/thinkcspy/SimplePythonData/OrderofOperations.html)

Using np stands for numpy,

```
1 / (1 + np.exp(-x))
```

> `1 / (1 + np.exp(-x))` - Same above, but `np.exp(-x)` will apply the exponential function to every element of x.

##### Sigmoid gradient

You will implement the function `sigmoid_grad()` to compute the gradient of the sigmoid function.

To compute the gradient of the sigmoid function, we need the sigmoid function we implemented last time.

```
s = sigmoid(x)
```

> `s = sigmoid(x)` - The previous `sigmoid` function assignes to variable `s`.

According to the derivative of sigmoid function,

```
ds = s * (1 - s)
```

> `ds = s * (1 - s)` - The derivative formula assgines to `ds` variable, stands for `ds/dx`.

##### Reshaping arrays

Reshape an image 3D array to a vector of shape (length*height*depth, 1).

```
v = image.reshape((image.shape[0]*image.shape[1]*image.shape[2], 1))
```

> `v = image.reshape((image.shape[0]*image.shape[1]*image.shape[2], 1))` - The `reshape` function takes tuple as a newshape (In this case, `(image.shape[0]*image.shape[1]*image.shape[2], 1)`).  
Reference: [numpy.reshape](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html#numpy.reshape)

##### Normalizing rows

To get a better performance, numpy matrix will be normalized with a value called norm.
Reference: [2.5 Norms](https://hadrienj.github.io/posts/Deep-Learning-Book-Series-2.5-Norms/)

Compute the norm 2 of x.

```
x_norm = np.linalg.norm(x, ord = 2, axis = 1, keepdims = True)
```

> `x_norm = np.linalg.norm(x, ord = 2, axis = 1, keepdims = True)` - Compute the Frobenius norm (`ord = 2`) each row of the matrix x (`axis = 1`) to normalize the rows of a matrix. The `keepdims` keep the result as dimensions with size one to broadcast correctly.  
> Reference: [numpy.linalg.norm](https://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.norm.html)

The x_norm will be

```
[[ 5.        ]
 [ 7.28010989]]
```

if x is

```
[[0, 3, 4],
 [1, 6, 4]]
```

##### Broadcasting and the softmax function

For the softmax for each row of the input x, Calculate the exponential of all each elements in the input array.

```
x_exp = np.exp(x)
```

Create a vector x_sum that sums each row of x_exp.

```
x_sum = np.sum(x_exp, axis = 1, keepdims = True)
```

> `x_sum = np.sum(x_exp, axis = 1, keepdims = True)` - Sum up the elements with arugument options that the same rule of `np.linalg.norm` function goes. x_sum is made up by `x_exp`.  
> Reference: [numpy.sum](https://docs.scipy.org/doc/numpy/reference/generated/numpy.sum.html)

##### Implement the L1 and L2 loss functions

The L1 loss function represents like in python:

```
loss = np.sum(abs(y - yhat))
```

> `loss = np.sum(abs(y - yhat))` -  The basic math python operations like `+、-、*、/` and `abs` are possible to use on a vector for each elements.  
Reference: [abs() in Python](https://www.geeksforgeeks.org/abs-in-python/)

Also the L2 loss function will be:

```
loss = np.dot(y-yhat, y-yhat)
```

> `loss = np.dot(y-yhat, y-yhat)` - x will be replaced by y-yhat.
