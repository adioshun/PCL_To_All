---
redirect_from:
  - "/guide/04-ros"
title: 'ROS'
prev_page:
  url: /guide/03_docker
  title: 'Docker 활용'
next_page:
  url: /01/intro_downsampling
  title: 'Down Sampling'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---
ROS파일에서 PCD파일 추출 하기


http://wiki.ros.org/pcl_ros

rosrun pcl_ros bag_to_pcd <input_file.bag> /<topic> <output_directory>
rosrun pcl_ros bag_to_pcd lobby_velodyne.bag /velodyne_points ./lobby_pcd
