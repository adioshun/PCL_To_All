---
redirect_from:
  - "/features/open3d"
interact_link: content/features/open3d.ipynb
title: 'Open3D (Python)'
prev_page:
  url: /features/markdown
  title: 'PCL (Python)'
next_page:
  url: /guide/01_overview
  title: '환경구성'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---



{:.input_area}
```python
import numpy as np
from open3d import *

import sys
sys.path.append("/workspace/include")

from visualization_helper import *

%matplotlib inline
```




{:.input_area}
```python
print("Testing IO for point cloud ...")
pcd = read_point_cloud("./../test.pcd")
print(pcd)
write_point_cloud("sample_secD.pcd", pcd)
write_point_cloud("test.pcd", pcd)
```


{:.output_stream}
```
Testing IO for point cloud ...
PointCloud with 2750 points.

```




{:.output_data_text}
```
True
```





{:.input_area}
```python
import k3d
```




{:.input_area}
```python
pa = np.asarray(pcd.points)

plot = k3d.plot()

points_number = pa.shape[0]
colors = np.random.randint(0, 0xFFFFFF, points_number)

points = k3d.points(pa, colors, point_size=0.01, shader='3d')
plot += points
plot.camera_auto_fit = False
plot.display()
```



{:.output_data_text}
```
Output()
```




{:.input_area}
```python
pa
```





{:.output_data_text}
```
array([[ 1.3579905 ,  4.00280809, -1.1325922 ],
       [ 3.33281803,  9.8181715 ,  0.18098146],
       [ 1.54550076,  4.55029202, -1.10945857],
       ...,
       [ 4.94497871, 12.22697258,  3.04493737],
       [ 4.00837469,  9.90613461, -0.18653132],
       [ 4.95058155, 12.22852612,  3.53495073]])
```





{:.input_area}
```python
pcd = PointCloud()
pcd.points = Vector3dVector(pa)
write_point_cloud("pa2pcd.pcd", pcd)
```





{:.output_data_text}
```
True
```





{:.input_area}
```python
pcd2 = read_point_cloud("pa2pcd.pcd")
```




{:.input_area}
```python
pcd2.colors
```





{:.output_data_text}
```
std::vector<Eigen::Vector3d> with 0 elements.
Use numpy.asarray() to access data.
```



# Cropping



{:.input_area}
```python
vol = read_selection_polygon_volume("cropped.json")

```




{:.input_area}
```python
chair = vol.crop_point_cloud(pcd)
```




{:.input_area}
```python
chair
```





{:.output_data_text}
```
PointCloud with 0 points.
```





{:.input_area}
```python
print("Recompute the normal of the downsampled point cloud")
estimate_normals(pcd, search_param = KDTreeSearchParamHybrid(
        radius = 0.1, max_nn = 30))
```


{:.output_stream}
```
Recompute the normal of the downsampled point cloud

```




{:.output_data_text}
```
True
```





{:.input_area}
```python
write_point_cloud("test.pcd", pcd)
```





{:.output_data_text}
```
True
```





{:.input_area}
```python
print("Load a ply point cloud, print it, and render it")
pcd = read_point_cloud("sample_table.pcd")
print(pcd)
print(np.asarray(pcd.points))

```


{:.output_stream}
```
Load a ply point cloud, print it, and render it
PointCloud with 460400 points.
[[-0.93387002 -0.6825     -1.18649995]
 [-0.93172997 -0.68322998 -1.18780005]
 [-0.92185003 -0.68054003 -1.18309999]
 ...
 [-0.12585001  0.38914001 -1.35699999]
 [-0.14683001  0.36662    -1.27849996]
 [-0.12884     0.37395999 -1.30410004]]

```



{:.input_area}
```python
draw_geometries([pcd])
```


# Normal Estimation



{:.input_area}
```python
normal = estimate_normals(pcd, search_param = KDTreeSearchParamHybrid(radius = 0.1, max_nn = 30))

```




{:.input_area}
```python
type(normal)
```





{:.output_data_text}
```
bool
```





{:.input_area}
```python
normal
```





{:.output_data_text}
```
True
```


