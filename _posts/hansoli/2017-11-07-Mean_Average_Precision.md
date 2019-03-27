---
layout: post
title: "mAP (Mean Average Precision)"
author: "정한솔"
date: 2017-11-07 12:00:00
categories: [Tutorials, Object Detection]
tags: [Object Detection]
---

이 포스트에서는 검색 알고리즘의 성능을 평가하는 지표 중 하나인 mAP(mean average precision)에 대하여 설명하겠습니다.

---

### 개요

mAP는 이진 분류기의 성능 지표로 사용되는 정밀도와 재현율을 이용한 지표이며 객체 검출 알고리즘의 성능을 평가하는데 널리 사용합니다.

 - 정밀도(Precision)는 양성으로 판정된 것 중 실제로 참인 것의 비율을 나타냅니다. '참 양성 / (참 양성 + 거짓 양성)'으로 정의됩니다.
 - 재현율(Recall)은 실제 값이 참인 것 중 판정이 양성인 것의 비율을 나타냅니다. '참 양성 / (참 양성 + 거짓 음성)'으로 정의됩니다.

재현율은 민감도(sensitivity)라는 이름으로도 불립니다.

딥러닝 객체 검출 알고리즘에서는 검출된 상자가 참일 가능성(확률)이 같이 출력됩니다. 확률이 몇 퍼센트 이상일 때 양성으로 판정할지의 기준선인 '임계값'을 몇으로 정하는지에 따라서 예측 결과가 참인지 거짓인지가 달라지기 때문에 정밀도와 재현율도 모두 달라지게 됩니다. 임계값을 바꿔가면서 실제로 참인 객체가 임계값 내에 포함될 때마다 정밀도와 재현율을 모두 측정하면 실제로 참인 객체 만큼의 정밀도, 재현율 쌍이 생기게 됩니다. 여기서 정밀도만을 골라 내어 평균을 낸 것이 평균 정밀도(AP; average precision)입니다.

객체 검출에서 출력되는 경계 박스는 참인지 거짓인지가 출력되지 않고 경계 박스의 위치만이 출력됩니다. 이 경계 박스를 실제로 참으로 볼지 거짓으로 볼지는 실체 위치(ground truth)와 검출된 객체 상자 간의 [IoU]({{ "/lecture/2017/09/28/IoU.html" | prepend: site.baseurl }}) 값이 일정 이상인지를 평가하여 이루어집니다.

mAP는 평균 정밀도를 다시 한번 더 평균 낸 값입니다. 분류기가 검출 가능한 각 분류 별로 정해진 테스트셋에서 평균 정밀도를 구하고 평균 정밀도를 다시 한번 더 평균 내면 mAP 값의 결과가 나오게 됩니다.

---

### 예제

파이썬 패키지 중 scikit-learn은 mAP를 계산하고 정밀도-재현율 그래프를 작성할 수 있는 기능을 제공하기 때문에 위 과정을 직접 구현할 필요는 없습니다.

```python
truths = []
scores = []

for img_path in images_path:
    detected_box = # 딥러닝 객체검출에서 검출된 경계박스
    prob = # 딥러닝 객체검출이 출력한 객체일 확률
    true_box = # 실제 객체의 위치에 대한 경계박스

    is_true = int(get_iou(detected_box, true_box) > 0.5)
    truths.append(is_true)
    scores.append(prob)
```

먼저 위와 같이 각 경계박스가 실제로 참인지 거짓인지를 나타내는 값을 0 또는 1로 가지고 있는 레이블 리스트와 객체 검출 알고리즘에서 출력된 확률을 담은 점수 리스트를 작성합니다. 여기서 get_iou는 두 경계 박스의 IoU를 구하는 사용자 정의 함수입니다.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import average_precision_score, precision_recall_curve

truths = np.array(truths)
scores = np.array(scores)

ap = average_precision_score(truths, scores)
print('평균 정밀도(AP)는 {}입니다.'.format(ap))

precision, recall, _ = precision_recall_curve(truths, scores)
plt.plot(recall, precision, color=colors[graphidx], label='{0} ({1:0.2f})'.format(key, ap), lw=2)\
plt.xlabel('Recall')
plt.ylabel('Precision')
plt.title('Precision-recall curve')
plt.ylim([0.0, 1.05])
plt.xlim([0.0, 1.0])
plt.legend(loc='lower left')
plt.savefig('prcurve.png')
```

그 후 두 리스트를 넘파이 배열로 변환한 다음에 위 예제 코드와 같이 average_precision_score, precision_recall_curve 함수에 인자로 넘겨주면 각각 평균 정밀도 값과, 그래프를 그리는데 사용할 수 있는 정밀도, 재현율 리스트를 얻을 수 있습니다.
