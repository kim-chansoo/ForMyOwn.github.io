---
layout: post
title:  "Weakly Supervised Learning of Rigid 3D Scene Flow"
date:   2024-01-14 19:31:29 +0900
categories: jekyll update
---

# 1. Introduction
3D scene flow는 Visual SLAM 분야의 2D optical flow의 일반화된 버전이라고 생각하면된다. raw point cloud를 사용해서 motion을 알아내는 기법이기 때문에, low-level scene을 representation한다고 표현하는 듯 하다. (정확히 3D scene flow의 의미를 이해 못함. 왜 high level에 motion perception이 존재?)high-level은 semantic segmentation이나 motion perception을 의미하는 듯 함. 3D

- 단점1: Vehicle의 non 적용시 불가능한 결과가 나올 수 있음.
- 단점2: Data driven이기 때문에, Data를 구축해야되고, Data 구축 시 비용이 많이 든다. 시뮬레이션 데이터를 사용하기도 하지만 domain gap이 발생한다.

## Contribution 제안
Scene abtraction 방법을 제안한다. Scene abtraction이란 movable object랑 static object를 구분하는 것을 의미한다. static object들의 움직임을 ego-motion으로 정의하고, moving object들의 cluster들을 rigidly moving entity로 정의한다. 그 결과 앞선 단점 1,2를 모두 극복할 수 있다. 1> static object의 움직임의 움직임 제약 조건을 강제하고, 2> binary mask annotation으로 대체 가능하게 한다. 

Contribution 정리
1. Weak supervision signal: background mask and ego-motion (상대적으로 적은 비용을 들여 얻을 수 있는 라벨, binary mask 사용)
2. moving/static을 분류: object 단위로 추론 가능
3. Backbone이 sceneflow여서 Various task에 적용가능(무엇이 새로운건지는 이해가 안되네요.)

# 2. Related Work

# 3. Method
$X$: $t_0$ point cloud
$Y$: $t_1$ point cloud
$V$: 객체들 --> K objects로 구성

# 3.1 Energy Formulation

$L_{BG}$: Bacg Ground (BG) Segmentation loss
Static/Dynamic을 binary class로 구분 log 이거 뭐더라 그 logarithm 러닝 방법 적용.

$L_{ego}$: ego-motion loss
entropy-regularized Sinkhorn algorithm 으로 point 사이의 data association을 진행.
1대1대응이 전부되지 않기 때문에 M-->A로 변경.
doubly stochastic assignment matrix가 나온ㄴ다고 함.
weighted Kabsch 알고리즘

$L_{FG}$: Fore ground loss

# 3.2 Network implementation

# 4. Experimental Evaluation