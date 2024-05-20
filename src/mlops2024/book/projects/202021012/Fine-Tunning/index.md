# 파인튜닝(Fine-tuning)

## 정의
파인튜닝은 특정 작업이나 도메인에 **높은 적합성을 확보**하기 위해, 이미 훈련된 대구모 언어 모델에 특정 데이터셋을 사용하여 **추가적인 학습을 수행**하는 작업을 말합니다. 즉, 기존에 학습되어져 있는 모델을 기반으로 아키텍처를 새로운 목적(나의 이미지 데이터에 맞게)에 맞게 변형하고 이미 학습된 모델 weight로 부터 학습을 업데이트 하는 방법입니다. 

- 모델의 파라미터를 미세하게 조정하는 행위
- '정교한'과 '파라미터'가 키포인트

파이튜닝의 핵심 아이디어는 머신러닝 모델이 초기 학습에서 **사용된 데이터만을 반영**한다는 점에서 비롯됩니다. 이에 따라 모델은 초기 학습 단계에서 다루지 않은 새로운 데이터 샘플을 이해하는 데 어려움을 겪을 수 있으며, 이는 **특정 상황에서 정확한 답을 생성하는 대규모 모델**에서 두드러집니다.

## 방법
파인튜닝은 사전학습된 모델 전체를 조정한 정도에 따라 **Full Fine-tuning**와 **Repurposing** 두 가지 방법으로 분류할 수 있습니다.

### Full Fine-tuning

Full Fine-tuning은 모든 매개변수를 포함하여 사전 학습된 **모델 전체를 파인튜닝하는 작업**을 의미합니다. 이 방법에서는 사전 학습된 모델의 모든 레이어와 매개 변수가 업데이트되고 최적화되어 대상 작업의 요구사항에 맞게 조정됩니다. 이 방법은 일반적으로 **작업과 사전 학습된 모델 사이에 큰 차이가 있거나 작업에서 모델의 유연성과 적응성이 높아야 하는 경우**에 적합니다. 전체 파인튜닝에는 상당한 리소스와 시간이 필요하지만 그만큼 더 나은 성능을 얻을 수 있습니다.

### Repurposing
Repurposing은 사전 학습된 모델의 **하위 레이어를 그대로 유지**하면서 모델의 상위 레이어 또는 선택된 **몇 개의 레이어를 파인 튜닝**하는 것을 의미합니다. 

이 방법의 목적은 사전 학습된 모델에 대한 **일반적인 지식을 유지**하면서 **최상위 레이어를 특정 작업에 적용**하는 것입니다. 이 방법은 대상 작업과 사전 학습된 모델 사이에 특정 **유사성**이 있거나 **작업 데이터셋이 작은 경우**에 적합한 경우가 많습니다. Repurposing은 몇 개의 레이어만 업데이트되므로 Full-tuning에 비해 필요한 리소스와 시간이 적지만 경우에 따라 약간의 성능 저하가 발생 할 수 있습니다. 

### 방법 비교
Full Fine-tuning과 Repurposing간의 선택은 작업의 특성과 사용 가능한 리소스에 따라 달라집니다. **작업과 사전학습된 모델 사이에 큰 차이**가 있거나 **높은 적응성이 필요**한 경우 Full Fine-tuning이 더 적합합니다. **작업이 사전 학습된 모델과 유사성**이 높거나 **리소스가 제한**적인 경우 Repurposing이 더 나은 선택일 수 있습니다. 실제 적용에서는 최적의 성능을 달성하기 위해 작업 요구 사항 및 실험 결과를 기반으로 적절한 파인 튜닝 방법을 선택해야 합니다.

## 데이터셋 유형별 파인 튜닝

LLM 파인튜닝은 사용되는 데이터셋 유형에 따라 지도 파인튜닝(Supervised Fine-tuning)과 비지도 파인튜닝(Unsupervised Fine-tuning)의 두 가지 유형으로 분류됩니다.

### 지도 파인튜닝(Supervised Fine-tuning)
지도 파인튜닝은 미세 조정 단계에서 레이블이 지정된 학습 데이터셋을 사용하는 프로세스를 의미합니다. 이때 레이블은 파인튜닝 중에 모델에 대한 목표 출력을 제공합니다. 지도 파인튜닝에서는 보통 각 샘플에 관련 레이블이 있는 분류 데이터셋과 같은 작업별 레이블이 지정된 데이터셋이 사용됩니다. 이러한 레이블을 활용하여 파인튜닝 프로세스를 안내하면 모델이 특정 작업에 더 잘 적응할 수 있습니다.

### 비지도 파인튜닝(Unsupervised Fine-tuning)
비지도 파인튜닝은 미세 조정 프로세스 중에 레이블이 지정되지 않은 학습 데이터셋을 사용하는 것을 포함합니다. 이는 모델이 명시적인 목표 출력 없이 입력 데이터 자체에 있는 정보에만 의존할 수 있음을 의미합니다. 이러한 방법은 유용한 기능을 추출하거나 모델의 표현 기능을 향상하는 것을 목표로 데이터의 고유 구조를 활용하거나 데이터를 생성하여 모델을 파인튜닝합니다.

### 비교
지도 파인튜닝은 일반적으로 레이블이 지정된 작업별 데이터셋에서 수행되므로 **모델 성능을 직접 최적화**할 수 있습니다. 반면, 비지도 파인튜닝은 더 유용한 특징 표현을 추출하거나 모델의 일반화 기능을 향상하기 위해 라벨링이 지정되지 않은 데이터를 사용하여 **특징 학습 및 표현 학습**에 더 **중점**을 둡니다. 이 두 가지 미세 조정 방법은 작업의 특성과 양, 사용 가능한 데이터에 따라 독립적으로 또는 조합하여 사용됩니다.

## 파인튜닝의 주요 단계
1. 데이터셋 준비
대상 작업과 관련된 학습 데이터셋을 수집하고 준비합니다. 데이터 세트의 품질과 정확성을 보장하고 필요한 데이터 정리 및 전처리를 수행합니다.

2. 사전 학습 및 파운데이션 모델 선택
대상 작업의 성격과 데이터셋의 특성을 기반으로 적합한 사전 학습 모델을 선택합니다.

3. 파인튜닝 전략 정의
작업 요구 사항 및 사용 가능한 리소스를 기반으로 적절한 파인튜닝 전략을 선택합니다. 전체 미세 조정을 수행할지 혹은 부분 미세 조정을 수행할지 여부와 파인튜닝 수준 및 범위를 고려합니다.

4. 하이퍼파라미터 설정
학습률, 배치 크기, 훈련 에포크 수 등과 같은 파인튜닝 프로세스를 위한 하이퍼파라미터를 결정합니다. 이러한 하이퍼파라미터의 선택은 미세 조정의 성능과 수렴 속도에 상당한 영향을 미칠 수 있습니다.

5.모델 매개변수 초기화
사전 학습된 모델의 가중치를 기반으로 파인튜닝된 모델의 매개변수를 초기화합니다. 완전한 미세 조정을 위해 모든 모델 매개변수가 무작위로 초기화됩니다. 부분 파인튜닝의 경우 최상위 레이어 또는 일부 레이어의 매개변수만 무작위로 초기화됩니다.

6. 파인튜닝 학습
준비한 데이터셋과 파인튜닝 전략을 사용하여 모델을 훈련합니다. 학습 과정에서 설정된 하이퍼파라미터와 최적화 알고리즘을 기반으로 모델 매개변수를 점진적으로 조정하여 손실 함수를 최소화합니다.

7. 모델 평가 및 튜닝
학습 과정에서 검증 세트를 사용하여 주기적으로 모델을 평가하고 평가 결과에 따라 하이퍼파라미터를 조정하거나 전략을 미세 조정합니다. 이는 모델의 성능과 일반화 능력을 향상하는 데 도움이 됩니다.

8. 모델 성능 테스트
미세 조정이 완료된 후 테스트 세트를 사용하여 최종 파인튜닝 모델을 평가하여 성능 지표를 얻습니다. 이는 실제 적용에서 모델의 성능을 평가하는 데 도움이 됩니다.

9. 모델 배포 및 적용
파인튜닝된 모델을 실제 응용 프로그램에 배포하고 실제 요구 사항을 충족하기 위해 추가 최적화 및 조정을 수행합니다.

이러한 단계는 LLM을 파인튜닝하기 위한 일반적인 프레임워크를 제공하지만, 특정 단계와 세부 사항은 작업 및 요구 사항에 따라 다를 수 있습니다. 특정 상황에 따라 조정 및 최적화가 이루어질 수 있습니다.

## 파인튜닝이 아닌 것
VGG16모델을 사용하여 고양이와 개 분류기를 만든다고 가정하겠습니다. VGG16모델은 1000개의 카테고리가 학습되어 있고 문제를 해결하기 위해서 모든 레이어를 사용할 필요가 없습니다. 따라서 몇 가지 수정을 거쳐야 하는 데 가장 쉽게 사용한다면 고양이와 개 이미지 사진을 해당 모델로 예측하여 보틀넥 피쳐만 뽑아내 어파인 레이어(Fully-connected layer)로 학습시키는 방법이 있습니다. 

이 경우 파인튜닝처럼 보일 수 있습니다. 하지만 파인튜닝은 모델의 파라미터를 미세하게 조절하는 행위, 즉 피쳐를 추출해내는 레이어의 파라미터를 업데이트하는 것이기 때문에 위 경우에는 파인튜닝이라고 보기 어렵습니다. 파인튜닝을 사용했다고 말하기 위해서는 기존에 학습된 레이어에 새로운 데이터를 추가로 학습시켜 파라미터를 업데이트 해야합니다. 



+ 번외
## 프롬프트 엔지니어링
프롬프트 엔지니어링은 파인튜닝과 함께 자연어처리 모델을 개선하는 데 사용되는 기술입니다. 프롬프트 엔지니어링의 경우 앞서 설명했던 파인튜닝과 비슷하지만 다른 기술로 기존의 모델을 변화시키지 않고, 모델의 입력에 적절한 프롬프트를 설계(특정한 문장을 추가)하여 모델의 출력을 개선하는 것을 의미합니다.

### 파인튜닝과 프롬프트 엔지니어링 비교
![파인튜닝-프롬프트엔지니어링비교](./파인튜닝-프롬프트엔지니어링비교.png)

**파인튜닝** 
- 모델 자체를 조정
- 모델의 가중치를 업데이트하여 새로운 작업에 맞게 조정
- 추가 학습을 통해 모델을 개선
- 대규모의 데이터세트를 사용하여 모델을 다시 학습시키는 과정을 포함

**프롬프트 엔지니어링**
- 입력을 조정
- 입력에 대해 적절한 가이드를 제공하여 모델 출력 개선
- 입력을 최적화
- 입력의 구성을 조정하여 모델 성능을 개선

### 파인튜닝과 프롬프트 엔지니어링의 장단점
파인튜닝의 장점
- 높은 성능
: 파인튜닝은 모델의 가중치를 조정하여 새로운 작업에 적합하게 만들기 때문에 높은 성능을 제공할 수 있습니다.
- 유연성
: 파인튜닝은 다양한 작업에 적용될 수 있으며, 특정 작업에 맞게 모델을 개선할 수 있습니다.

파인튜닝의 단점
- 학습 시간과 비용
: 파인튜닝은 추가 학습을 필요로 하기 때문에 학습 시간과 비용이 증가할 수 있습니다.
- 네트워크 용량
: 파인튜닝 된 모델은 원래 모델보다 더 많은 메모리 및 디스크 공간을 필요로 할 수 있습니다.

프롬프트 엔지니어링의 장점
- 빠른 적용
: 프롬프트 엔지니어링은 입력의 조정을 통해 빠르게 모델의 성능을 개선할 수 있습니다.
- 고성능 모델의 활용
: 프롬프트 엔지니어링은 이미 고성능 모델을 활용할 수 있는 경우에 유용합니다.

프롬프트 엔지니어링의 단점
- 모델 의존성
: 프롬프트 엔지니어링은 모델의 입력에 대한 조정으로 성능을 개선하기 때문에 모델에 의존적입니다.
- 프롬프트 설계의 어려움
: 적절한 프롬프트를 설계하는 것은 어려울 수 있으며, 실험과 반복적인 작업을 필요로 합니다.

## 정리
프롬프트 엔지니어링은 모델의 출력을 조작하기 위해 사용되고, 파인 튜닝은 새로운 작업에 대한 예측 정확도를 높이기 위해 사용된다. 파인튜닝은 특화된 작업에 높은 성능이 요구될 때 필요하다. 

파인튜닝이 유용할 때
- 일관된 대답을 원할 때
- 모델의 능력을 극대화하고 싶을 때
- 특정 주제에 대한 지식을 높이고 싶을 때
- 오류나 틀린 정보를 수정하고 싶을 때

[reference]

[파인튜닝(Fine-tuning)이란?](https://kr.appen.com/blog/fine-tuning/)

[pre-training 과 fine-tuning (파인튜닝)](https://eehoeskrap.tistory.com/186)

파인튜닝과 프롬프트 엔지니어링](https://www.toolify.ai/ko/ai-news-kr/i5by7anfngh095ifwgrcp9la4je51aom-945655)