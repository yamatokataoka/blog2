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

# Week 2

Key Concepts on Programming Assignments
- Work with iPython Notebooks
- Become familiar with Python and Numpy
- Implement the main steps of an ML algorithm, including making predictions, derivative computation, and gradient descent.
- Build a logistic regression model, structured as a shallow neural network
- Be able to implement vectorization across multiple training examples
- Implement computationally efficient, highly vectorized, versions of models.

## Python Basics with numpy

In this assignment you will:

- Learn how to use numpy.
- Implement some basic core deep learning functions such as the softmax, sigmoid, dsigmoid, etc...
- Learn how to handle data by normalizing inputs and reshaping images.
- Recognize the importance of vectorization.
- Understand how python broadcasting works.

### sigmoid function, np.exp()

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

### Sigmoid gradient

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

### Reshaping arrays

Reshape an image 3D array to a vector of shape (length*height*depth, 1).

```
v = image.reshape((image.shape[0]*image.shape[1]*image.shape[2], 1))
```

> `v = image.reshape((image.shape[0]*image.shape[1]*image.shape[2], 1))` - The `reshape` function takes tuple as a newshape (In this case, `(image.shape[0]*image.shape[1]*image.shape[2], 1)`).  
Reference: [numpy.reshape](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html#numpy.reshape)

### Normalizing rows

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

### Broadcasting and the softmax function

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

### Implement the L1 and L2 loss functions

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

## Logistic Regression with a Neural Network mindset

You will implement:
- The general architecture of a learning algorithm
- The cost function and its gradient
- The optimization algorithm (gradient descent)

### Packages

Import a helper package to load dataset provided by Coursera deeplearning.ai.

```
from lr_utils import load_dataset
```

and run a matplotlib magic function to include matplotlib graphs in your notebook.  
Reference: [Purpose of “%matplotlib inline”](https://stackoverflow.com/questions/43027980/purpose-of-matplotlib-inline)

```
%matplotlib inline
```

### Overview of the Problem set

You can check the original picture using `matplotlib.pyplot` library.

```
plt.imshow(train_set_x_orig[index])
```

> `plt.imshow(train_set_x_orig[index])` - Display an image as a (M, N, 3): an image with RGB values.  
> Reference: [matplotlib.pyplot.imshow](https://matplotlib.org/3.1.3/api/_as_gen/matplotlib.pyplot.imshow.html)

For the input features, we can select all rows and the specific column index  by specifying `:` for in the rows index, and `index` variable in the columns index.  
Reference: [Two-Dimensional Slicing](https://machinelearningmastery.com/index-slice-reshape-numpy-arrays-machine-learning-python/)

```
train_set_y[:, index]
```

FYI, you can check `train_set_y` ndarray shape.

```
print(str(train_set_y.shape))
```

```
(1, 209)
```

Also check the `classes` array.

```
print(classes)
```

```
[b'non-cat' b'cat']
```

> `b'non-cat'` - Python 3 uses unicode, and marks bytestrings with this b.  
> Reference: ['b' character added when using numpy loadtxt](https://stackoverflow.com/questions/33655641/b-character-added-when-using-numpy-loadtxt)

You can decode utf-8 by

```
decode("utf-8")
```

And using `np.squeeze` function, the ndarray becomes zero dimension ndarray.  
Reference: [Zero-dimensional numpy.ndarray : only element is a 2D array : how to access it?](https://stackoverflow.com/questions/51149865/zero-dimensional-numpy-ndarray-only-element-is-a-2d-array-how-to-access-it)

```
np.squeeze(train_set_y[:, index])
```

> `np.squeeze` - Remove single-dimensional entries from the shape of an array.  
> Reference: [numpy.squeeze](https://docs.scipy.org/doc/numpy/reference/generated/numpy.squeeze.html)

The shape print `()` tuple.

```
print(np.squeeze(train_set_y[:, index]).shape)
```

To flatten the image training set,

```
train_set_x_orig.reshape(m_train, -1).T
```

> `train_set_x_orig.reshape(m_train, -1)` - Reshape the original ndarray, `train_set_x_orig` to `(m_train, -1)` column as `m_train` but rows as unknown. The `-1` is used when it is unknown. The `T` transpose the shape from `(m_train, 12288)` to `(12288, m_train)`.  
> Reference: [What does -1 mean in numpy reshape?](https://stackoverflow.com/questions/18691084/what-does-1-mean-in-numpy-reshape)

The sanity check shows you how your pixel array should end up by sampling a few elements. If you are wrong ways to do the reshape and flatten, which would end up with the pixels in a different order.

### Building the parts of our algorithm

For parameter initialization of w, we can use `np.zeros` function with specifying the shape, `(dim, 1)`.  
Reference: [numpy.zeros](https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros.html)

```
w = np.zeros((dim, 1))
```

For forward propagation (computing current loss), first implement using the activation function, sigmoid function here.  
Reference: [What is a Neural Network Activation Function?](https://missinglink.ai/guides/neural-network-concepts/7-types-neural-network-activation-functions-right/)

```
sigmoid(np.dot(w.T, X) + b)
```

> `np.dot(w.T, X)` - Compute dot product of two arrays. w is stack horizontally, so transpose it using `.T`.  
> Reference: [numpy.dot](https://docs.scipy.org/doc/numpy/reference/generated/numpy.dot.html)

In that case of w = `np.array([[1.],[2.]])`, b = `2.`, and X = `np.array([[1.,2.,-1.],[3.,4.,-3.2]])`, the result would be

```
[[ 0.99987661  0.99999386  0.00449627]]
```

Next, compute cost, the difference between Y and computed A

```
cost = -1 / m * (np.sum(Y*np.log(A) + (1-Y)*np.log(1-A)))
```

Then computes current gradient as a backward propagation using pre-calculated two formulas.

For w

```
1 / m * np.dot(X, (A-Y).T)
```

For b

```
1 / m * np.sum(A - Y)
```

Those slopes will change w and b to reduce loss, cose result. So optimize it using those.

For example, in case of w using `learning_rate` and `dw`

```
w = w - learning_rate*dw
```

Uisng those learned w and b, make a prediction. Convert the entries of a into 0 (if activation <= 0.5) or 1 (if activation > 0.5), stores the predictions in a vector Y_prediction.

```
if A[:, i] >= 0.5:
    Y_prediction[:, i] = 1.
else:
    Y_prediction[:, i] = 0.
```

### Merge all functions into a model

Here, you see how to compute the test accuracy.

```
100 - np.mean(np.abs(Y_prediction_test - Y_test)) * 100)
```

> `Y_prediction_test - Y_test` - The difference between predicted result and real value.
>
> `np.mean(np.abs(Y_prediction_test - Y_test))` - So, this computes the overall meaning of loss.
>
> `100 - np.mean(np.abs(Y_prediction_test - Y_test)) * 100)` - 100 - loss = accuracy.
