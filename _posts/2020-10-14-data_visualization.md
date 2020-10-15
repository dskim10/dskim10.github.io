---
title: "데이터 시각화"
date: 2017-10-20 08:26:28 -0400
tags:
    - DataAnalysis
---
ML에서 자주 사용되는 데이터 시각화 도구와 사용방법에 대해 알아보자.

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# [matplotlib](https://matplotlib.org/)
Matplotlib은 파이썬에서 MATLAB과 유사한 인터페이스로 그래프를 표시하기 위해 사용되는 라이브러리다.
 <!-- 2002년 존 헌터(John Hunter)에 의해 개발 되기 시작했고, 이후 -->

## Figure와 Subplot
matplotlib에서 그래프는 Figure 객체 내에 존재한다.
```python
import numpy as np
from numpy.random import randn
import matplotlib.pyplot as plt

# Figure 객체 생성
fig = plt.figure()

# Figure에 subplot 추가
ax1 = fig.add_subplot(2, 2, 1)
ax2 = fig.add_subplot(2, 2, 2)
ax3 = fig.add_subplot(2, 2, 3)

# 현재 활성화된 Figure의 subplot에 그린다. 'k--'는 검을 점선 스타일 지정.  
plt.plot(randn(50).cumsum(), 'k--')
plt.show()
```
결과
<!-- ![](post/2020-10-14-data_visualization/Figure_1.png?raw=true) -->
<center><img src = "/assets/images/2020-10-14-data_visualization_figure_1.png" width = "640"></center><br>

'fig.add_subplot'에서 반환되는 객체는 AxesSubplot 객체이다. 현재 활성화된 객체가 아닌 각각의 인스턴스 객체에 아래와 같이 직접 그래프를 그릴 수도 있다.
```python
_ = ax1.hist(randn(100), bins=20, color='k', alpha=0.3)
ax2.scatter(np.arange(30), np.arange(30) + 3 * randn(30))
```
<center><img src = "/assets/images/2020-10-14-data_visualization_figure_2.png" width = "640"></center><br>

보통은 다음과 같이 특정한 배치를 가지도록 여러 개의 서브플롯을 포함하는 Figure를 한번에 생성한다.
```python
fig, axes = plt.subplots(2, 3)
```
axes 배열에 저장된 AxesSubplot 인스턴스에는 'axes[0, 1]'처럼 2차원 배열 인덱스로 접근할 수 있다.

## 라벨, 범례

```python
fig, axes = plt.subplots(1, 2)
# {'b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'}
axes[0].plot(randn(1000).cumsum(), 'k', label='one')
axes[0].plot(randn(1000).cumsum(), 'g--', label='two')
axes[0].plot(randn(1000).cumsum(), 'b.', label='three')
axes[0].set_title('Figure 1. My First Plot')
axes[0].set_xlabel('Stages')
axes[0].legend(loc='best')

# {'tab:blue', 'tab:orange', 'tab:green', 'tab:red', 'tab:purple', 'tab:brown', 'tab:pink',
# 'tab:gray', 'tab:olive', 'tab:cyan'} (case-insensitive)
axes[1].plot(randn(1000).cumsum(), 'tab:orange', label='one')
axes[1].plot(randn(1000).cumsum(), 'tab:purple', label='two')
axes[1].plot(randn(1000).cumsum(), 'tab:blue', label='three')
axes[1].set_title('Figure 1. My Second Plot')
axes[1].set_xlabel('Stages')
axes[1].legend(loc='best')

plt.show()
```
<center><img src = "/assets/images/2020-10-14-data_visualization_figure_3.png" width = "800"></center><br>

## 틱 설정
우선 싸인, 코싸인 그래프를 그려보자.
```python
fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)

# 각축의 표시 범위 지정
ax.set_xlim([-3.5, 3.5])
ax.set_ylim([-1.2, 1.2])

x = np.linspace(-np.pi, np.pi, 200)
siny = np.sin(x)
cosy = np.cos(x)
ax.plot(x, siny, 'tab:red', linewidth=1.5)
ax.plot(x, cosy, 'tab:blue', linewidth=1.5)
```
<center><img src = "/assets/images/2020-10-14-data_visualization_figure_4.png" width = "640"></center><br>

x축의 눈금 $$\pi$$단위로 보기 좋게 변경해 보자. 
```python
fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)

# 각축의 표시 범위 지정
ax.set_xlim([-3.5, 3.5])
ax.set_ylim([-1.2, 1.2])

# x축의 눈금 변경하기, 눈금 라벨표시에 'LaTeX 문법'을 사용할 수 있다.
ax.set_xticks([-np.pi, -np.pi / 2, 0, np.pi / 2, np.pi])
ax.set_xticklabels(['$-\pi$', '$-\pi/2$', '$0$', '$\pi/2$', '$\pi$'])

x = np.linspace(-np.pi, np.pi, 200)
siny = np.sin(x)
cosy = np.cos(x)
ax.plot(x, siny, 'tab:red', linewidth=1.5)
ax.plot(x, cosy, 'tab:blue', linewidth=1.5)
```
<center><img src = "/assets/images/2020-10-14-data_visualization_figure_5.png" width = "640"></center><br>



<!-- # [seaborn](https://seaborn.pydata.org/) -->

