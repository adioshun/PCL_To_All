---
redirect_from:
  - "/02/1/passthrough-filter"
interact_link: content/02/1/PassThrough_filter.ipynb
title: 'PassThrough filter'
prev_page:
  url: /02/intro_filtering
  title: 'RoI Filtering'
next_page:
  url: /03/intro_noise
  title: 'Noise Filtering'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

## PassThrough Filter

본 챕터에서는 RoI 추출 방법 중 하나인 PassThrough Filter에 대하여 다루고 있습니다. 

PassThrough Filter는 입력값으로 관심 영역의 x,y,z의 최대/최소값을 받아 crop하는 방식으로, 직관적이지만 정교한 부분을 제거하지는 못하는 단점이 있습니다. 

자세한 내용은 [Filtering a PointCloud using a PassThrough filter](http://pointclouds.org/documentation/tutorials/passthrough.php#passthrough)를 참고 하시면 됩니다.  




{:.input_area}
```python
%load_ext watermark
%watermark -d -v -p pcl,numpy
```


{:.output_stream}
```
2018-11-23 

CPython 3.5.2
IPython 6.4.0

pcl unknown
numpy 1.14.5

```



{:.input_area}
```python
# -*- coding: utf-8 -*-
from __future__ import print_function
import pcl
import numpy as np

import os
os.chdir("/workspace/3D_People_Detection_Tracking") 
```




{:.input_area}
```python
from include.visualization_helper import *
%matplotlib inline
```


## PassThough Filter 정의

입력 
- pcl_data : point cloud
- filter_axis : 제거할 축 (x or y or z)
- axis_min : 최소 크기
- axis_max : 최대 크기

출력  
- point cloud



{:.input_area}
```python
def do_passthrough(pcl_data,filter_axis,axis_min,axis_max):
    '''
    Create a PassThrough  object and assigns a filter axis and range.
    :param pcl_data: point could data subscriber
    :param filter_axis: filter axis
    :param axis_min: Minimum  axis to the passthrough filter object
    :param axis_max: Maximum axis to the passthrough filter object
    :return: passthrough on point cloud
    :https://github.com/fouliex/RoboticPerception
    '''
    passthrough = pcl_data.make_passthrough_filter()
    passthrough.set_filter_field_name(filter_axis)
    passthrough.set_filter_limits(axis_min, axis_max)
    return passthrough.filter()
```


## PCD 파일 읽기



{:.input_area}
```python
cloud = pcl.load("./sample/lobby.pcd") # Deprecated; use pcl.load instead.
print(cloud)
```


{:.output_stream}
```
<PointCloud of 19329 points>

```



{:.input_area}
```python
visualization2D_xyz(cloud.to_array())
```


{:.output_stream}
```
(x) : 92.2m
(y) : 87.5m
(z) : 10.3m

```


![png](../../images/02/1/PassThrough_filter_8_1.png)


## PassThough Filter 수행



{:.input_area}
```python
filter_axis = 'x'
axis_min = 1.0
axis_max = 20.0
cloud = do_passthrough(cloud, filter_axis, axis_min, axis_max)
```




{:.input_area}
```python
visualization2D_xyz(cloud.to_array())
```


{:.output_stream}
```
(x) : 19.0m
(y) : 87.5m
(z) : 8.7m

```


![png](../../images/02/1/PassThrough_filter_11_1.png)




{:.input_area}
```python
filter_axis = 'y'
axis_min = -7.0
axis_max = 5.5
cloud = do_passthrough(cloud, filter_axis, axis_min, axis_max)
```




{:.input_area}
```python
visualization2D_xyz(cloud.to_array())
```


{:.output_stream}
```
(x) : 19.0m
(y) : 12.5m
(z) : 2.3m

```


![png](../../images/02/1/PassThrough_filter_13_1.png)




{:.input_area}
```python
visualization3D_xyz(cloud.to_array())
```


{:.output_stream}
```
(x) : 19.0m
(y) : 12.5m
(z) : 2.3m

```


![png](../../images/02/1/PassThrough_filter_14_1.png)




{:.input_area}
```python
filter_axis = 'z'
axis_min = -1.2
axis_max = 10.0
cloud = do_passthrough(cloud, filter_axis, axis_min, axis_max)
```




{:.input_area}
```python
visualization3D_xyz(cloud.to_array())
```


{:.output_stream}
```
(x) : 2.7m
(y) : 9.8m
(z) : 1.5m

```


![png](../../images/02/1/PassThrough_filter_16_1.png)


> PassThrough필터의 z축 필터링을 통해서 바닥제거도 가능합니다. 
> 단, Lidar가 기울어져있으면 근거리와 원거리의 z값이 다르기 때문에 설치시 조심해야 합니다. 
