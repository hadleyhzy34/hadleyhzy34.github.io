---
layout: post
title: Python File System Module
key: 20201113
tags:
  - Python
  - glob
  - pathlib
---


## Glob Module

```python
import glob
import cv2

data = []
files = glob.glob("source/*.jpg")
for file in files:
    image = cv2.imread(file)
    img = cv2.resize(image, (400,600), interpolation = cv2.INTER_AREA)
    data.append(img)
```



<!--more-->

## Pathlib Module

```python
from pathlib import Path
import cv2

path_str = '/Users/hadley/Pictures/'

for path in Path(path_str).rglob('*.jpg'):
    _dir = '{}'.format(path)
    img = cv2.imread(_dir)
    if img.shape[0] > img.shape[1]:
        img = cv2.rotate(img, cv2.ROTATE_90_COUNTERCLOCKWISE)
        cv2.imwrite(_dir, img)
        print(_dir)
    # print(path.absolute)
```

* path.name: return file name
* path: return path + file name

Note that none of above return string format, convert it into string format then use OpenCV module.
{:.warning}





