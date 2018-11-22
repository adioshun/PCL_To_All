---
redirect_from:
  - "/features/open3d"
interact_link: content/features/open3d.ipynb
title: 'Open3D (Python)'
prev_page:
  url: /features/python-pcl
  title: 'PCL (Python)'
next_page:
  url: /guide/01_overview
  title: '환경구성'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

## Open3D
- 본 챕터에서는 Open3D 기본적인 파일 입력, Numpy변환, 저장 방법에 대하여 정리 하였습니다. 



{:.input_area}
```python
%load_ext watermark
%watermark -d -v -p numpy
```


{:.output_stream}
```
2018-11-22 

CPython 2.7.12
IPython 5.8.0

numpy 1.15.4

```



{:.input_area}
```python
import open3d
import numpy as np

import os
os.chdir("/workspace/3D_People_Detection_Tracking") 
print("Open3D Version : {}".format(open3d.__version__))
```


{:.output_stream}
```
Open3D Version : 0.4.0.0

```

## Point cloud 생성

### 배열로 생성



{:.input_area}
```python
pc_array = np.array([[1, 2, 3], [3, 4, 5]], dtype=np.float32)
print(pc_array)
```


{:.output_stream}
```
[[1. 2. 3.]
 [3. 4. 5.]]

```



{:.input_area}
```python
pc = open3d.PointCloud()
pc.points = open3d.Vector3dVector(pc_array)
print(pc)
```


{:.output_stream}
```
PointCloud with 2 points.

```

### PCD 파일 읽기



{:.input_area}
```python
pc = open3d.read_point_cloud("./sample/lobby.pcd") 
print(pc)
```


{:.output_stream}
```
PointCloud with 19329 points.

```

### txt 파일 읽기



{:.input_area}
```python
!cat ./sample/open3d_xyz.txt
```


{:.output_stream}
```
0.0000000000 0.0000000000 0.0000000000
1.0000000000 0.0000000000 0.0000000000
0.0000000000 1.0000000000 0.0000000000
0.0000000000 0.0000000000 1.0000000000

```



{:.input_area}
```python
open3d.read_point_cloud("./sample/open3d_xyz.txt", format='xyz')
```





{:.output_data_text}
```
PointCloud with 4 points.
```



## 정보 확인



{:.input_area}
```python
print("포인트 수 : {}".format(pc.dimension))
```


{:.output_stream}
```
포인트 수 : <bound method PointCloud.dimension of PointCloud with 19329 points.>

```



{:.input_area}
```python
#print ('Loaded ' + str(pc.width * pc.height) + ' data points from test_pcd.pcd with the following fields: ')

for i in range(0, 10):
    print ('x: ' + str(pc.points[i][0]) + ', y : ' + str(pc.points[i][1]) + ', z : ' + str(pc.points[i][2]))

```


{:.output_stream}
```
x: 5.555420875549316, y : 0.7530959844589233, z : -1.5021858215332031
x: 36.19226837158203, y : 4.899829387664795, z : 0.6375014781951904
x: 6.652876377105713, y : 0.8995062112808228, z : -1.5499128103256226
x: 23.42300033569336, y : 3.162747383117676, z : 1.238687515258789
x: 8.198750495910645, y : 1.1070561408996582, z : -1.6081383228302002
x: 23.224275588989258, y : 3.131787061691284, z : 2.0502514839172363
x: 10.736045837402344, y : 1.4458502531051636, z : -1.715773344039917
x: 23.25834846496582, y : 3.1281161308288574, z : 2.881479024887085
x: 15.359683990478516, y : 2.063061475753784, z : -1.9028680324554443
x: 32.76459503173828, y : 4.38918924331665, z : 6.425684452056885

```

## Numpy로 변환

- 추후 군집화, 분류, 전처리를 위해서 일반적으로 Numpy로 변환 하여 작업을 수행 



{:.input_area}
```python
pc_array = np.asarray(pc.points)
print("pc Type : {}".format(type(pc)))
print("pc_array Type : {}".format(type(pc_array)))
```


{:.output_stream}
```
pc Type : <class 'open3d.open3d.PointCloud'>
pc_array Type : <type 'numpy.ndarray'>

```

### Numpy 기반 정보 출력



{:.input_area}
```python
print("pc_array shape : {}".format(pc_array.shape))
print("pc_array size : {}".format(pc_array.size))
print("pc_array ndim : {}".format(pc_array.ndim))
print("pc_array dtype : {}".format(pc_array.dtype))
print("pc_array nbytes : {} bytes".format(pc_array.nbytes))
```


{:.output_stream}
```
pc_array shape : (19329, 3)
pc_array size : 57987
pc_array ndim : 2
pc_array dtype : float64
pc_array nbytes : 463896 bytes

```

## pcd로 저장

### point cloud를 pcd로 저장



{:.input_area}
```python
open3d.write_point_cloud("pc2pcd.pcd", pc)
#The supported extension names are: pcd, ply, xyz, xyzrgb, xyzn, pts.
```





{:.output_data_text}
```
True
```



### numpy를 pcd로 저장



{:.input_area}
```python
pc_new = open3d.PointCloud()
pc_new.points = open3d.Vector3dVector(pc_array)
open3d.write_point_cloud("pc2pcd.pcd", pc_new)
```





{:.output_data_text}
```
True
```


