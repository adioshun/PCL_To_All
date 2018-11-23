---
redirect_from:
  - "/03/intro-noise"
title: 'Noise(=Outlier) Filtering'
prev_page:
  url: /02/2/conditional_filter
  title: 'Conditional filter'
next_page:
  url: /03/2/radius_filter
  title: 'Radius Outlier filter'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---
Noise Filtering
=====================

Lidar는 센서 특성상 물체가 존재 하지 않아도 먼지등으로 인해 point가 생성 됩니다. 이렇게 생성된 point들을 Noise로 간주 하고 제거 하는 작업을 진행 해야 합니다.

다행히 이러한 노이즈들은 정상적인 ponint 대비 빈 공간에 소수의 점들만 탐지 되므로 이러한 특성을 이용하여 제거 할수 있습니다.

- Statistical based

- Radius based


> **[중요]** 현재 Radius based 방식은 정상 동작 하지 않는다고 합니다. 파라미터를 바꾸어도 결과가 '0'이라고 하네요. [[참고]](https://github.com/strawlab/python-pcl/issues/211) - 2018.06.11
