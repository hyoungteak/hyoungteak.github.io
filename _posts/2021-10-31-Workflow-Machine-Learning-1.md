---
title:  "머신러닝 워크플로우(workflow of machine learning) - 1"
excerpt: "머신러닝 일반적인 워크플로우(The universal workflow of machine learning)와 작업 정의(Define the task), 모델 개발(Develop a model)"

categories:
 - AI
tags:
 - [machine learning]

toc: true
toc_sticky: true

date: 2021-10-31
last_modified_at: 2021-10-31
---

# **1. 머신러닝의 일반적인 워크플로우(The universal workflow of machine learning)**

머신러닝의 워크플로우는 보편적으로 세 부분으로 구성됩니다.

 - **작업 정의(Define the task)**: 기계 학습 문제를 구성하는 단계 - 고객의 질문의 근저에 있는 문제 도메인과 비즈니스 로직을 이해합니다. 데이터 셋을 수집하여 데이터가 무엇을 나타내는지 이해하고 작업 성공을 어떻게 측정할 것인지 선택합니다.

 - **모델 개발(Develop a model)**: 작업 모델 개발 단계 - 머신러닝 모델에서 데이터를 처리할 수 있도록 준비하고, 모델 평가 프로토콜과 단순한 베이스라인을 선택하여, 지나치게 적합한 일반화 능력을 가진 최초의 모델을 훈련하고, 가능한 최고의 일반화 성능을 달성할 때까지 모델을 정규화하고 조정합니다.

 - **모델 도입(Deploy the model)**: 운영 시 모델을 배치하고 유지하는 단계 - 작업 내용을 관계자에게 제시하고 모델을 웹 서버, 모바일 애플리케이션, 웹 페이지 또는 임베디드 디바이스에 전송하여 모델의 야외 퍼포먼스를 감시하고 차세대 모델 구축에 필요한 데이터 수집을 시작합니다.

---

> **참고: 머신러닝의 윤리에 대해**
>
>머신러닝을 배울 때, 시작할 레이블이 지정된 데이터 세트가 있고 모델 훈련을 시작하는 데, 실제로는 문제에서 시작하는 경우가 기본적입니다. 책에서는 사진 검색엔진, 텍스트 스팸, 카드 감지 등 여러 가지 분야에서 머신러닝이 활용되고 있습니다.
>
>또한, 윤리 관련해서 '얼굴 사진으로 신뢰도를 평가하는 AI'와 같은 타당성이 있는지 의심되는 프로젝트도 진행할 수 있는데, 왜 신뢰성이 누군가의 얼굴에 반영되는지 명확하지 않을뿐더러 이런 작업은 모든 종류의 윤리적인 문제를 제기합니다.
>
>어떤 특정 인물이 이 사람은 신뢰할 수 없다고 말하는 것보다 AI가 이 사람은 신뢰할 수 없다하는 것이 더 비중과 객관성을 띄는 것으로 보이기 때문에 우리가 제작하는 모델은 사람 판단의 부정적인 면을 제외하고 동작시키고, 부정적인 영향을 끼칠 수 있습니다.
>
>결론적으론, 기술은 절대 중립일 수 없고 우리가 제작한 모델이 세상에 도덕적인 영향을 끼칠 수 있기 때문에 항상 제작되는 모델, 기술 등에서 고민하고 주의하여 훈련, 제작에 힘써야 합니다.

---

## **1.1. 작업 정의(Define the task)**

자신이 하고 있는 작업의 문제를 깊이 이해하지 않으면 좋은 작업을 할 수 없습니다. 고객들은 왜 이 특정한 문제를 해결하려고 하고, 고객은 솔루션에서 어떤 가치를 얻을지, 제작 모델은 어떻게 사용되며, 비즈니스 과정에 얼마나 적합한지 등의 고민이 있을 수 있습니다. 머신러닝 문제를 구성하려면 일반적으로 이해 관계자(stakeholders)와 상세한 논의가 필요합니다.

---

### **1.1.1. 문제 구성(Frame the problem)**

 - 데이터 가용성(data availability)이 제한요인이 된다.
입력 데이터나 무엇을 예측하려는 것인지에 따라서 대부분 새로운 데이터셋을 가져오고, 스스로 특성을 붙여야 합니다.

 - 어떤 유형의 기계 학습 작업을 선택할 것인지 고민해야 한다.
예를 들면, 사진 검색은 멀티클래스, 멀티라벨 분류, 스팸 탐지는 이진분류 작업이다. 데이터의 종류나 어떤 문제냐에 따라 선택해야 할 작업이 다릅니다.

 - 기존 솔루션이 무엇인지 생각해야 한다.
사람의 수작업으로 진행되는 공정과정을 보면 어떤 시스템이 이미 도입되었고, 어떤 기능을 하고 있는지 이해해야 합니다.

 - 처리해야 할 특정한 제약이 있는지 찾아야 한다.
예를 들어 스팸 검출 시스템을 구축하고 있는 애플리케이션은 end-to-end에서 암호화 되어있기 때문에, 외부 데이터 세트로 훈련해야 합니다. 즉, 하고자 하는 작업의 전체적인 맥락을 파악해야 합니다.

이렇게 조사가 완료되면 입력내용(input), 목표(target) 및 문제가 어떤 종류의 머신러닝(machine learning) 작업에 매핑(mapping)되는지 파악해야 합니다.

단, 이 단계에서 작성한 가설에 주의해야 합니다.

 - 입력을 고려하여 목표를 예측할 수 있다고 가정한다.

 - 사용가능한(또는 바로 수집하는) 데이터는 입력과 목표의 관계를 학습하기에 충분한 정보라고 가정한다.

실제 모델이 만들어질 때까지 위 내용은 단순한 가설일 뿐, 검증(validated) 또는 무효화(invalidated)를 작업을 기다리고 있습니다. 머신 러닝으로 모든 문제를 해결할 수 있는 것은 아닙니다. 입력 값 X와 목표인 Y를 조립한다고 해서 X가 Y를 예측하기에 충분한 정보를 포함하고 있는 것은 아닙니다.

---

### **1.1.2. 데이터 세트 수집(Collect a dataset)**

작업을 이해하고, 입력과 목표가 무엇인지를 이해한다면, 머신러닝 프로젝트에서 가장 어렵고 시간‧비용이 많이 드는 데이터 수집의 단계로 넘어갑니다. 예를 들면, 사진 검색 엔진 프로젝트에서는 먼저 분류 라벨 세트를 선택해야 합니다. 10,000의 일반적인 이미지 카테고리로 설정합니다. 다음으로 사용자가 업로드한 수십만의 이미지에 이 세트의 라벨을 수동으로 태그 붙여야 합니다.

모델의 일반화 능력은 훈련된 데이터의 특성, 즉 데이터 포인트 수, 레이블의 신뢰성, 기능의 품질에서 나옵니다. 훌륭한 데이터 셋은 주의해서 투자할 만한 자산입니다. 프로젝트가 50시간 더 소요될 경우 모델링 개선점을 찾을 것이 아니라 더 많은 데이터를 수집하는 것이 가장 효과적인 방법일 수 있습니다.

알고리즘보다 데이터가 중요하다는 점은 구글 연구자에 의한 2009년 논문 "The Unreasonable Effectiveness of Data“에서부터 유명해졌습니다. 이는 딥러닝 학습이 유명해지기 전의 일이지만 놀랍게도 딥러닝의 대두는 데이터의 중요성을 더 키웠습니다.

지도학습을 하는 경우 입력(이미지 등)을 수집하면 그 입력(이미지 태그 등)에 대한 주석이 필요합니다. 이것은 예측할 수 있는 것처럼 모델을 훈련하는 목표물입니다.

주석은 음악 추천 작업이나 선택 예측 작업의 경우 자동으로 수집되지만, 종종 수작업으로 데이터에 주석을 달아주어야 합니다. 이 과정은 노동력이 많이 드는 과정(labor-heavy process)입니다.

---

**데이터-주석 인프라 투자(Investing in data-annotation infrastructure)**

데이터 주석 프로세스에 의해 목표의 품질이 결정되고 모델의 품질이 결정됩니다. 사용 가능한 옵션을 충분히 검토해야합니다.
 - 데이터에 직접 주석을 달아야 하는지

 - 라벨 수집을 위해 메카니컬 터크(Mechanical Turk: 컴퓨터로 대응할 수 없지만 인간의 지능을 활용하면 쉬운 과업같은 느낌)와 같은 클라우드 소싱 플랫폼(crowdsourcing platform)을 사용해야 하는지

 - 데이터 라벨 전문 회사의 서비스를 이용해야 하는지

아웃소싱을 통해 시간과 비용을 절약할 수 있지만 본인이 관리할 수는 없게 됩니다. 메카니컬 터크(Mechanical Turk)를 사용하는 것은 저렴하게 확장할 수 있지만, 주석은 꽤 시끄러울 수 있습니다.

최적의 옵션을 선택하려면, 다음 제약을 고려해야 합니다.

 - 데이터 라벨기가 대상 분야에 대해 전문성을 띄어야 하는지, 고양이와 개의 이미지 분류 문제의 라벨은 누구라도 선택할 수 있지만 견종 분류 작업의 라벨은 전문 지식이 필요하다. 또한, 골절의 CT 검사에서 주석을 달기 위해서는 의학 학위가 필요합니다.

 - 데이터에 주석을 달기 위해 전문 지식이 필요한 경우 사람이 주석을 달기 위해 훈련시킬 수 있는지, 그렇지 않으면 어떻게 관련 전문가와 접촉할 수 있는지

 - 전문가들이 주석을 다는 것을 이해할 수 있는지, 그렇지 않으면 데이터 셋을 블랙박스(결과는 원하는 대로 도출하지만, 근거를 알 수 없는 것)로 취급해야 하며 수동기능 엔지니어링(manual feature engineering)을 수행할 수 없습니다. 이는 중요하진 않지만 제한적일 수 있습니다.

---

**비대표적 데이터 주의(Beware of non-representative data)**

머신 러닝 모델은 이전에 본 것과 같은 입력 만 이해할 수 있습니다. 교육(Train) 데이터는 생산(Production) 데이터를 대표하지 않기 때문에 트레이닝에 사용하는 데이터가 실제 데이터를 대표하는 것이 중요합니다. 이 문제는 모든 데이터 수집 작업의 기초가 됩니다.

가능하면 모델이 사용될 환경에서 직접 데이터를 수집합니다. 영화 감상 분류 모델은 Yelp 레스토랑 리뷰나 Twitter 상태 업데이트가 아닌 새로운 IMDB(인터넷 영화 데이터베이스) 리뷰에 사용되어야 합니다. 생산 데이터에 대한 훈련이 가능하지 않다면, **훈련 데이터와 생산 데이터가 어떻게 다른지 완전히 이해**하고 이러한 차이를 적극적으로 수정해야 합니다.

주의해야 할 관련현상은 **개념 드리프트**(**Conceept drift**: 시간이 지남에 따라 모델링 대상의 통계적 특성이 바뀌는 현상)입니다. 거의 모든 현실적인 문제, 특히 사용자가 생성한 데이터를 다루는 문제로 개념의 변화에 직면하게 되면 생산 데이터의 특성이 시간과 함께 변화하면서 모델 정확도가 서서히 저하될 때 발생합니다. 개념 드리프트를 처리하려면 지속적인 데이터 수집, 주석, 모델 재훈련이 필요하다.

머신러닝은 훈련 데이터에 포함된 패턴을 기억하기 위해서만 사용될 수 있다는 점에 유의해야 합니다. 전에 본 것밖에 인식하지 못하기 때문에, 과거의 데이터를 바탕으로 훈련된 머신러닝을 사용하여 미래를 예측하는 것은 미래가 과거와 같이 행동할 것이라고 가정하는 것입니다.

---

>**참고: 샘플링 편향의 문제(SAMPLING BIAS)**
>
>비대표적 데이터의 내재적이고 일반적인 케이스는 샘플링 편향이다. 샘플링 편향은 데이터 수집 프로세스가 예측하고자 하는 것과 상호작용하여 편향된 측정이 이루어질 때 발생합니다. 예를 들자면 선거 전, 여론 조사를 특정 지역, 특정 나이만 조사한다면, 당연히 편향된 측정이 이루어질 수밖에 없습니다.

---

### **1.1.3. 데이터 이해하기(Understand your data)**

데이터 셋을 블랙박스로 취급하는 것은 좋지 않습니다. 훈련 모델을 시작하기 전에 데이터를 조사하고 시각화하고 예측 가능한 정보를 얻어야 합니다. 예측 가능한 정보는 기능 엔지니어링(feature engineering) 및 잠재적인 문제 선별(screen for potential issues)에 도움이 됩니다.

예를 들어, 데이터에 이미지나 자연어 텍스트가 포함된 경우는, 몇 가지 샘플(및 해당 레이블)을 직접 확인해야 합니다. 그 외 숫자 형상, 위치 정보 등을 파악하는 것이 좋습니다.

**목표 누설(target leaking)** 여부를 확인합니다. 실가동 환경에서 사용할 수 없는 목표에 대한 정보를 제공하는 기능이 데이터에 포함되어 있는지 확인해야 합니다.

앞으로 누군가가 암의 치료를 받을지 예측하기 위해 모델을 훈련하고 있는 경우, 기록에 “이 사람이 암으로 진단되었다”라는 특징이 포함되어 있으면, 목표물이 인위적으로 데이터에 유출되고 있는 것입니다. 데이터의 모든 기능이 운영 환경에서도 동일한 형태로 제공되는지 항상 주의해야 합니다.

---

### **1.1.4. 성공의 척도 선택(Choose a measure of success)**

무언가를 통제하려면 그것을 관찰할 수 있어야 합니다. 프로젝트에서 성공을 거두려면 먼저 성공-정확성(success-accuracy)이란 무엇인가를 정의해야 합니다. 정확성과 리콜, 고객 유지율 등 성공을 위한 지표는 프로젝트 전반을 통틀어 수행하는 모든 기술적 선택의 지침이 됩니다. 이는 고객의 성공적인 비즈니스 등 보다 높은 수준의 목표에 직접 부합해야 합니다.

머신러닝 성공지표(machine-learning success metrics)의 다양성과 이러한 메트릭이 서로 다른 문제영역과 어떻게 관련되어 있는지 공부하려면 캐글(Kaggle)에서 데이터 사이언스 대회를 참고하는 것이 도움이 됩니다. 다양한 문제와 평가지표를 볼 수 있습니다.

---

## **1.2. 모델 개발(Develop a model)**

진행 상황을 어떻게 측정할지 알면 모델 개발을 시작할 수 있습니다. 대부분의 튜토리얼과 연구 프로젝트는 이미 수행되었다고 가정한 문제 정의 및 데이터 세트 수집을 건너뛰고, 다른 사람이 처리한 것으로 가정하는 모델 배치 및 유지보수를 건너뛴다고 가정합니다. 사실 모델 개발은 기계 학습 워크플로우 중 한 단계일 뿐입니다.

---

### **1.2.1. 데이터 준비(Prepare the data)**

앞에서 배웠듯 딥러닝 모델은 일반적으로 기존 데이터를 수집하지 않습니다. 데이터 전처리는 갖고 있는 원시 데이터를 신경망에 쉽게 적응할 수 있도록 하는 것을 목표로 합니다. 여기엔 벡터화, 정규화 또는 결측값 처리가 포함됩니다. 많은 전처리 기술은 도메인마다 다릅니다(예: 텍스트 데이터 또는 이미지 데이터). 모든 데이터 도메인에 공통적으로 적용되는 기본 사항에 대해 살펴보도록 합시다.

---

**벡터화(Vectorization)**

신경망(neural network)의 모든 입력과 목표는 일반적으로 부동소수점 데이터의 텐서(또는 특정 경우의 정수나 문자열의 텐서)여야 합니다. 소리, 이미지, 텍스트 등 필요한 데이터가 무엇이든 먼저 텐서로 변환해야 합니다. 이 단계를 데이터 벡터화라고 합니다. 예를 들어, 두 텍스트 분류 예에서는 정수 목록(단어 시퀀스를 나타냄)으로 표현된 텍스트에서 시작하여 원-핫 인코딩(one-hot encoding)을 사용하여 float32 데이터의 텐서로 변환합니다.

---

**값 정규화(Value normalization)**

MNIST 숫자 분류 예제에서는 0-255 범위의 정수로 인코딩된 이미지 데이터에서 시작하여 그레이스케일(grayscale) 값을 인코딩했습니다. 이 데이터를 네트워크에 입력하기 전에 부동소수점 값이 0-1 범위에 오르게 하려면 부동소수점 값을 float32로 캐스팅하고 255로 나누어야 합니다.

상대적으로 큰 값(예: 네트워크의 초기 가중치보다 훨씬 큰 여러 자리 정수)을 사용하는 신경망 데이터나 이종 데이터(heterogeneous data)(예: 한 특징이 0-1이고 다른 특징이 100-200인 데이터)에 입력하는 것은 안전하지 않습니다. 이렇게 하면 대규모 그라데이션 업데이트가 트리거되어 네트워크가 수렴되지 않을 수 있습니다. 네트워크에서 보다 쉽게 학습하려면 데이터에 다음과 같은 특성이 있어야 합니다.

 - **작은 값 사용(Take small values)**: 일반적으로 대부분의 값은 0-1 범위여야 합니다.
 - **균일성(homogeneous)**: 즉, 모든 특성(feature)이 거의 동일한 범위의 값을 가져야 합니다.

또한 다음과 같은 엄격한 정규화 방법이 항상 필요한 것은 아니지만 도움이 될 수 있습니다.

 - 평균이 0이 되도록 각 피쳐를 독립적으로 정규화합니다.
 - 표준 편차가 1이 되도록 각 형상을 독립적으로 정규화합니다.

넘파이(NumPy) 어레이에선 이 작업을 쉽게 수행할 수 있습니다.

---

**결측값 처리(Handling missing values)**

종종 데이터에 결측값이 있을 수 있습니다. 예를 들어, House-price 예제 첫 번째 특징(인덱스가 0인 열)은 1인당 범죄율이었는데, 만약 이 기능이 모든 샘플에서 사용할 수 없다면 훈련 또는 테스트 데이터에 결측값이 있게 됩니다.
결측값 데이터를 완전히 폐기할 수도 있지만 반드시 할 필요는 없습니다.

 - 범주형 특성인 경우, 값이 누락되었다는 것을 의미하는 새 범주를 작성하는 것이 안전합니다. 모델은 대상에 대해 자동으로 학습하게 됩니다.
 - 수치형 특성의 경우, 0과 같은 임의 값을 입력하면 훈련된 모델이 일반화하기 더 어려워질 수 있으므로, 결측값을 데이터의 평균값 또는 중간값으로 바꾸는 것을 고려해야 합니다.

테스트 데이터에서 네트워크가 결측값 없이 데이터에 대해 학습된 경우, 네트워크는 결측값을 무시하는 방법을 배우지 않습니다. 이 경우 누락된 항목이 있는 훈련 샘플을 인위적으로 생성해야 합니다. 일부 훈련 샘플을 여러 번 복사하고 테스트 데이터에서 누락될 것으로 예상되는 범주형 특성 중 일부를 삭제해야 합니다.

---

### **1.2.2. 평가 프로토콜 선택(Choose an evaluation protocol)**

모델의 목적은 일반화를 달성하는 것이며, 모델 개발 프로세스 전반에 걸쳐 내릴 모든 모델링 결정은 일반화 성과를 측정하기 위한 검증 지표(validation metric)에 의해 진행됩니다. 검증 프로토콜의 목표는 실제 생산 데이터에서 선택한 성공 지표(예: 정확도)를 정확하게 추정하는 것입니다. 그 과정의 신뢰성은 유용한 모델을 구축하는 데 매우 중요합니다.

일반적으로 사용하는 세 가지 평가 프로토콜을 알아볼 수 있습니다.

 - **홀드아웃 유효성 검사 세트(hold-out validation set)**: 데이터가 많을 때 사용하는 방법

 - **K-겹 교차 검증(K-fold cross-validation)**: 샘플 수가 너무 적어서 홀드아웃 검증을 신뢰할 수 없을 때 사용

 - **반복 K-겹 검증(iterated K-fold validation)**: 데이터가 거의 없을 때 매우 정확한 모델 평가 수행

대부분의 경우 첫 번째 방법은 충분히 효과가 있을 것입니다. 앞에서 배웠듯, 항상 검증 세트의 대표성에 유의하고 훈련 세트와 검증 세트 사이에 중복 샘플이 없도록 주의해야 합니다.

---

### **1.2.3. 기준선 능가(Beat a baseline)**

모델 자체에 대한 작업을 시작하면 **통계적 검정력**을 달성하는 것이 초기 목표입니다. 즉, 간단한 기준선을 능가할 수 있는 작은 모델을 개발하는 것입니다.

이 단계에서 가장 중요한 세 가지 사항은 다음과 같습니다.

 - 특성 엔지니어링을 통해 정보를 제공하지 않는 특성(특성 선택)을 필터링하고 문제에 대한 지식을 활용하여, 사용할 수 있는 새로운 특성을 만들 수 있습니다.
 - 올바른 이전 아키텍처 선택: 촘촘하게 연결된 네트워크, 반복적인 신경 네트워크 등 과업에 대한 좋은 접근법이 있는지 아니면 다른 것을 사용해야 하는지 판단해야 합니다.
 - 훈련 환경 설정: 손실 함수(loss function), 배치크기(batch size), 학습율(learning rate) 등을 알맞게 설정해야 합니다.

---

>**참고: 올바른 손실 함수 선택(PICKING THE RIGHT LOSS FUNCTION)**
>
>문제에 대한 정확도를 측정하는 메트릭에 대해 직접적으로 최적화하지 못하는 경우가 많습니다. 메트릭을 손실 함수로 바꾸는 쉬운 방법이 없을 때도 있습니다. 결국 손실 함수는 데이터의 미니배치(이상적으로 손실 함수는 단일 데이터 포인트만큼만 계산 가능해야 함)가 주어져야 하며, 역전파를 사용하여 네트워크를 훈련시킬 수 없어야 합니다.
>
>아래 표는 일반적인 문제 유형에 대한 마지막 계층 활성화 및 손실 함수를 선택하는 데 도움이 될 수 있습니다.

 | Problem type | Last-layer activation | Loss function |
|:----------|:----------:|----------:|
| Binary classification | sigmoid | binary_crossentropy |
| Multiclass, single-label classification | softmax | categorical_crossentropy |
| Multiclass, multilabel classification | sigmoid | binary_crossentropy |
| Regression to arbitrary values | None | mse |

---

검정력을 가지는 것은 항상 가능한 것은 아닙니다. 합리적인 아키텍처를 여러 번 시도해도 단순한 기준선을 넘을 수 없다면 입력 데이터에 질문에 대한 답이 없는 것일 수 있습니다. 이 경우 두 가지 문제점을 확인할 수 있습니다.

 - 입력이 주어지면 출력을 예측할 수 있다.
 - 사용 가능한 데이터가 입력과 출력 간의 관계를 학습하는 데 충분한 정보를 제공한다.

이 가설들은 거짓일 가능성이 높으며, 이 경우 처음부터 다시 시작해야 합니다.

---

### **1.2.4 스케일 업: 과적합 모델 개발(Scale up: develop a model that overfits)**

검정력을 가진 모델을 만들면, 보통 과연 모델이 충분히 강력한가를 확인할 것입니다. 먼저 문제 해결을 위해 적절하게 모델링하기에 충분한 레이어와 파라미터를 가지고 있는지 확인해야 합니다. 머신러닝은 최적화와 일반화 사이를 적절하게 유지해야 합니다. 이상적인 모델은 과소적합과 과적합, 과소용량과 과용량 사이의 경계에 서 있는 모델입니다.

얼마나 큰 모델이 필요한지 알아내려면, 과적합 모델을 만들면 됩니다. 레이어를 추가하고, 층을 크게 만들고, 훈련 횟수(epochs)를 더 늘립니다. 훈련 손실 및 검증 손실은 물론이고 메트릭에 대한 교육 및 검증 값도 항상 모니터링합니다. 검증 데이터에 대한 모델의 성능이 저하되기 시작하면 과적합이 이루어진 것입니다.

---

### **1.2.5 모델 정규화 및 튜닝(Regularize and tune your model)**

일단 모델이 검정력과 과적합이 되면, 이 단계부터 일반화 성능을 최대화하는 것이 목표입니다.

이 단계에서 모델이 최대한 좋은 결과를 얻을 때까지 반복적으로 모델을 수정하고 훈련하고 검증 데이터(현 시점, 테스트 데이터가 아님)를 평가한 다음 다시 수정하고 반복합니다. 다음과 같은 몇 가지 방법을 시도해볼 수 있습니다.

 - 다른 아키텍처를 시도하거나 레이어를 추가 또는 제거합니다. 또는 드롭아웃(Dropout: 랜덤 노드 선택)을 추가합니다.
 - 모델이 작으면 L1 또는 L2 정규화를 추가합니다.
 - 최적의 구성을 찾기 위해 다양한 하이퍼 파라미터를 사용할 수 있습니다.
 - 선택적으로 데이터 큐레이션(data curation) 또는 특성 엔지니어링(feature engineering)을 반복할 수 있습니다. 더 많은 데이터를 수집하고 주석을 달거나, 더 나은 특성을 개발하거나, 유용한 것으로 보이지 않는 특성을 제거할 수 있습니다.

케라스튜너(KerasTuner)와 같이 자동화된 하이퍼 파라미터 튜닝 소프트웨어를 사용하여 이 작업의 상당 부분을 자동화할 수 있습니다.

검증 프로세스의 피드백을 사용하여 모델을 설정할 때마다 검증 프로세스에 대한 정보가 모델에 들어가게 됩니다. 몇 번만 반복하는 것은 무해하지만, 여러 반복에 걸쳐 체계적으로 수행되면 검증 데이터에 대해 직접 교육을 받은 모델이 없음에도 불구하고 결국 모델이 검증 프로세스에 과도하게 적합하게 됩니다. 이러한 행동은 평가 과정의 신뢰성을 떨어뜨립니다.

만족스러운 모델 구성을 개발하면, 사용 가능한 모든 데이터(훈련 및 검증)에 대해 최종 생산 모델을 훈련하고 테스트 세트에서 마지막으로 평가할 수 있습니다. 테스트 세트의 성능이 검증 데이터에서 측정된 성능보다 훨씬 더 나쁜 것으로 판명되면 이는 검증 절차를 신뢰할 수 없거나 모델의 매개 변수를 조정하는 동안 검증 데이터에 과적합하기 시작했음을 의미할 수 있습니다. 이 경우 K-겹 반복 유효성 검사처럼 안정적인 평가 프로토콜로 전환할 수 있습니다.
