---
layout: post
title: Convolutional Neural Network from Scratch, Keras&Tensorflow
key: 20201115
tags:
  - Python
  - CNN
  - deep learning
  - tensorflow
---

## image I/O

### `cv2.imread()`

Syntax: cv2.imread(path, flag)

Parameters:
1. path
2. flag: It specifies the way in which image should be read. It's default value is **cv2.IMREAD_COLOR**  

**cv2.IMREAD_COLOR**:It specifies to load a color image, default flag, alternatively, we can pass 1 for this flag.

**cv2.IMREAD_GRAYSCALE**: It specifies to load an image in grayscale mode. Alternatively pass value 0.

**cv2.IMREAD_UNCHANGED**: It specifies to load an image including alpha channel.

{:.info}

Return Value: returns an image





## image basic operation

### rotate `cv2.rotate()`

Syntax: cv2.rotate(src, rotateCode)

Parameters:

1. src: t is the image whose color space is to be changed

2. rotateCode: It is an enum to specify how to rotate the array.

  * cv2.ROTATE_()\_CLOCKWISE
  * cv2.ROTATE_()\_COUNTERCLOCKWISE
  * cv2.ROTATE_180

Return value: It returns an image