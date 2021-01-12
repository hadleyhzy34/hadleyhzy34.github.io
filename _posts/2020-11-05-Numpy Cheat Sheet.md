---
layout: post
title: Python Numpy Cheat Sheet
key: 20201105
tags:
  - Python
  - Numpy
  - data structure
---  

## numpy.array()

### array initialization

#### array initialization using list

``` python
>>> arr = np.array([1,2,3,4,5])
>>> arr
array([1, 2, 3, 4, 5])
>>> print(arr)
[1 2 3 4 5]
>>> print(type(arr))   
<class 'numpy.ndarray'>
```
<!--more-->

#### array initialization using tuple

```python
>>> arr = np.array((1,2,3,4,5))
>>> print(arr)
[1 2 3 4 5]
>>> print(type(arr))
<class 'numpy.ndarray'>
```

#### multiple dimension array initialization

```python
>>> arr = np.array([[1,2,3],[4,5,6]])        #2D array
>>> print(arr)
[[1 2 3]
 [4 5 6]]
>>> arr = np.array([[1,2,3],[4,5,6],[7,8,9]])   #3D array
>>> print(arr)
[[1 2 3]
 [4 5 6]
 [7 8 9]]
>>> print(arr.ndim)
2
>>> arr = np.array([1,2,3,4,5],ndmin=5)
>>> print(arr)
[[[[[1 2 3 4 5]]]]]
>>> print(arr.ndim)
5
```

#### array initialization using numpy.arange()

```python
>>> arr = np.arange(10)
>>> print(arr)
[0 1 2 3 4 5 6 7 8 9]
>>> arr = np.arange(2,10,dtype=float)    #array data type provided
>>> print(arr)
[2. 3. 4. 5. 6. 7. 8. 9.]
>>> np.arange(2,3,0.3)            #array data increment value provided
array([2. , 2.3, 2.6, 2.9])
```

#### array initialization using numpy.linspace()

```python
>>> arr = np.linspace(1,10,3)       #specified number of elements
>>> print(arr)
[ 1.   5.5 10. ]
```
#### array initialization with specified value/pattern

```python
>>> arr = np.zeros((3,3))
>>> print(arr)
[[0. 0. 0.]
 [0. 0. 0.]
 [0. 0. 0.]]
>>> arr = np.ones((3,3))
>>> print(arr)
[[1. 1. 1.]
 [1. 1. 1.]
 [1. 1. 1.]]
>>> arr = np.eye(3)
>>> print(arr)
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
>>> import random
>>> arr = np.random.random((5,5))
>>> print(arr)
[[0.93339097 0.81709556 0.22525984 0.05647321 0.19215437]
 [0.03587774 0.09410721 0.25606215 0.48443578 0.23163535]
 [0.70446729 0.47863469 0.19481695 0.10812323 0.11235218]
 [0.58988559 0.10543337 0.76473581 0.16447926 0.91451755]
 [0.52786593 0.03281677 0.05107855 0.78931466 0.75653137]]
>>> arr = np.full((3,3),-1)
>>> print(arr)
[[-1 -1 -1]
 [-1 -1 -1]
 [-1 -1 -1]]
>>> i,j = np.indices((3,4))
>>> print(i)                       #element value equals to current row idx
[[0 0 0 0]
 [1 1 1 1]
 [2 2 2 2]]
>>> print(j)                 #element value equals to current col idx
[[0 1 2 3]
 [0 1 2 3]
 [0 1 2 3]]
>>> arr = np.indices((3,4))
>>> print(arr)
[[[0 0 0 0]
  [1 1 1 1]
  [2 2 2 2]]

 [[0 1 2 3]
  [0 1 2 3]
  [0 1 2 3]]]
```

### array attribute

#### shape
```python
>>> arr = np.array([[1,2,3],[4,5,6]])
>>> print(arr.shape)
(2, 3)
>>> arr = np.array([1,2,3])
>>> print(arr.shape)
(3,)
>>> arr = np.array([[1],[2],[3]])
>>> print(arr.shape)
(3, 1)
```

#### reshape
```python
>>> x = np.array([[1,2,3],[4,5,6]])
>>> print(x.shape)
(2, 3)
>>> y = np.reshape(x,(3,2))
>>> print(y)
[[1 2]
 [3 4]
 [5 6]]
>>> z = np.array([1,2,3])
>>> print(z.shape)
(3,)
>>> m = np.reshape(z,(3,1))
>>> print(m)
[[1]
 [2]
 [3]]
>>> n = np.reshape(m,(3))
>>> print(n)
[1 2 3]
```

#### dtype

```python
>>> x = np.array([1,2,3])
>>> print(x.dtype)
int64
>>> x = np.array([1.,2.,3.])
>>> print(x.dtype)
float64
>>> x = np.array([1,2],dtype=float)
>>> print(x)
[1. 2.]
>>> print(x.dtype)
float64
```

### array indexing & slicing

#### single index

```python
>>> x = np.arange(10)
>>> x[0]
0
>>> x[9]
9
>>> x[10]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: index 10 is out of bounds for axis 0 with size 10
>>> x[-1]
9
``` 

#### modification of slice of array

a slice of array is a view into the same data, so modifying it will modify the original array.

```python
>>> arr = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
>>> x = arr[0:2,1:3]
>>> print(x)
[[2 3]
 [6 7]]
>>> x[0,1]=100
>>> print(arr)
[[  1   2 100   4]
 [  5   6   7   8]
 [  9  10  11  12]]
``` 
#### mix integer indexing with slice

```python
>>> print(arr)
[[  1   2 100   4]
 [  5   6   7   8]
 [  9  10  11  12]]
>>> x = arr[1,:]
>>> y = arr[1:2,:]
>>> print(x,x.shape)
[5 6 7 8] (4,)
>>> print(y,y.shape)
[[5 6 7 8]] (1, 4)
>>> x = arr[:,1]
>>> y = arr[:,1:2]
>>> print(x,x.shape)
[ 2  6 10] (3,)
>>> print(y,y.shape)
[[ 2]
 [ 6]
 [10]] (3, 1)
```

#### integer array indexing

```python
>>> arr
array([[  1,   2, 100,   4],
       [  5,   6,   7,   8],
       [  9,  10,  11,  12]])
>>> x = arr[[0,1,2],[0,1,0]]
>>> print(x)
[1 6 9]
>>> x = np.array([arr[0,0],arr[1,1],arr[0,2]])
>>> print(x)
[  1   6 100]
>>> x = arr[range(3),[0,1,2]]
>>> print(x)
[ 1  6 11]
>>> arr[range(3),[2,1,0]] += 100
>>> print(arr)
[[  1   2 200   4]
 [  5 106   7   8]
 [109  10  11  12]]
```

#### boolean array indexing

```python
>>> print(arr)
[[  1   2 200   4]
 [  5 106   7   8]
 [109  10  11  12]]
>>> print((arr>2))
[[False False  True  True]
 [ True  True  True  True]
 [ True  True  True  True]]
>>> print(arr[arr>2])           #construct a rank 1 array
[200   4   5 106   7   8 109  10  11  12]
```


### array basic operation

#### dot

this function returns the dot product of two arrays. For 2-D vectors, it is equivalent to matrix multiplication. For 1-D vectors, it is the inner product of the vectors.

1. If both a and b are 1-D arrays, it is inner product of vectors (without complex conjugation).
 2. If both a and b are 2-D arrays, it is matrix multiplication, but using matmul or a @ b is preferred.
 3. If either a or b is 0-D (scalar), it is equivalent to multiply and using numpy.multiply(a, b) or a * b is preferred.
 4. If a is an N-D array and b is a 1-D array, it is a sum product over the last axis of a and b.

 {:.info}

 When a or b is 2D array while the other is 1D array, it still applies to maxtrix multiplication rules.
 {:.warning}
 

```python
>>> v = np.array([9,10])
>>> w = np.array([11,12])
>>> print(v.dot(w))
219
>>> np.dot(v,w)
219
>>> x= np.array([[1,2],[3,4]])
>>> print(np.dot(w,v))
219
>>> print(np.dot(x,v))
[29 67]
>>> print(x.dot(v))
[29 67]
>>> y = np.array([[5,6],[7,8]])
>>> print(np.dot(x,y))
[[19 22]
 [43 50]]
```

#### sum

```python
>>> x
array([[1, 2],
       [3, 4]])
>>> print(sum(x))
[4 6]
>>> print(np.sum(x))
10
>>> print(np.sum(x,axis=0))
[4 6]
>>> print(np.sum(x,axis=1))
[3 7]
>>> print(np.sum(x,axis=(0,1)))
10
```

#### transpose

```python
>>> x = np.array([1,2,3])
>>> print(x.shape)
(3,)
>>> y = x.T
>>> print(y)
[1 2 3]
>>> print(y.shape)
(3,)

>>> x = np.array([[1,2,3],[4,5,6]])
>>> print(x)
[[1 2 3]
 [4 5 6]]
>>> y = x.T
>>> print(y)
[[1 4]
 [2 5]
 [3 6]]
>>> print(y.shape)
(3, 2)
>>> print(x.shape)
(2, 3)
```

Note that 1D array after transpose is still 1D array.
{:.warning}

#### broadcasting

Broadcasting is a powerful mechanism that allows numpy to work with arrays of different shapes when performing arithmetic operations. Frequently we have a smaller array and a larger array, and we want to use the smaller array multiple times to perform some operation on the larger array.

```python
>>> x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
>>> v = np.array([-1,-2,-3])
>>> y=x+v
>>> print(y)
[[0 0 0]
 [3 3 3]
 [6 6 6]
 [9 9 9]]
```

#### reference
https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html

When operating on two arrays, NumPy compares their shapes element-wise. It starts with the trailing dimensions, and works its way forward. Two dimensions are compatible when

* they are equal, or
* one of them is 1

When either of the dimensions compared is one, the other is used. In other words, dimensions with size 1 are stretched or “copied” to match the other.

temp * w => dimension(3,1) * dimension(2) => dimension(3,2) * dimension(2)
=> np.array([[1,1],[2,2],[3,3]]) * np.array([4,5])

v * w_reshape => dimension(3) * dimension(2,1) => dimension(3) * dimension(2,3) => np.array([1,2,3]) * np.array([[4,4,4],[5,5,5]])


```python
>>> v = np.array([1,2,3])
>>> w = np.array([4,5])
>>> temp = np.reshape(v,(3,1))
>>> w_reshape = np.reshape(w,(2,1))
>>> print(np.reshape(v,(3,1)) * w)
[[ 4  5]
 [ 8 10]
 [12 15]]
>>> print(v * np.reshape(w,(2,1)))
[[ 4  8 12]
 [ 5 10 15]]
```
```
[[1],
 [2],
 [3]]
```
transferred to below when computing `np.reshape(v,(3,1)) * w`:

```
[[1,1],
 [2,2],
 [3,3]]
```

```python
>>> print(x)
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]
>>> print(x*2)
[[ 2  4  6]
 [ 8 10 12]
 [14 16 18]
 [20 22 24]]
>>> print(x**2)
[[  1   4   9]
 [ 16  25  36]
 [ 49  64  81]
 [100 121 144]]
```

#### array unique 

```python
>>> arr = np.array([1,1,1,1,2,2,2,3,3,4])
>>> val,counts = np.unique(arr,return_counts=True)
>>> print(val,type(val))
[1 2 3 4] <class 'numpy.ndarray'>
>>> print(counts,type(counts))
[4 3 2 1] <class 'numpy.ndarray'>
```

#### array and list conversion


### array math

#### basic

```python
>>> x = np.array([1,2,3])
>>> y = np.array([4,5,6])
>>> print(np.add(x,y))
[5 7 9]
>>> print(np.subtract(x,y))
[-3 -3 -3]
>>> x = np.array([[1,2,3],[4,5,6]])
>>> y = np.array([[1,2,3],[4,5,6]])
>>> print(x*y)
[[ 1  4  9]
 [16 25 36]]
>>> print(np.multiply(x,y))
[[ 1  4  9]
 [16 25 36]]
>>> print(x/y)
[[1. 1. 1.]
 [1. 1. 1.]]
>>> print(np.divide(x,y))
[[1. 1. 1.]
 [1. 1. 1.]]
>>> print(x//y)
[[1 1 1]
 [1 1 1]]
>>> print(np.sqrt(x))
[[1.         1.41421356 1.73205081]
 [2.         2.23606798 2.44948974]]
```

