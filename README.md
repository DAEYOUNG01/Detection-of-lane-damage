# 도로 손상 객체 검출 시스템(Detection_of_lane_damage)
---


# CONTENTS


* **프로젝트 제목** : 프로젝트의 간략한 이름 및 설명

  
* **프로젝트 개요** : 프로젝트에 대한 전반적인 설명(배경, 목적, 제안 이유)

  
* **도로 훼손 객체 탐지 알고리즘 설계** : 알고리즘 설계에 대한 내용


* **모델 설계**

  
* **프로젝트 결과**


* **프로젝트의 한계 및 향후 연구 방향**


* **기대효과** 
---


# 프로젝트 제목 : SegRoad

SegRoad는 도로 이미지에서 손상된 부분을 정확하게 검출하기 위한 세그멘테이션 기반 시스템이다.

이를 통해 도로 유지보수 효율성을 높이고, 안전한 주행 환경을 제공한다.

SegRoad는 자율주행 차량을 위한 중요한 데이터 소스로 활용될 수 있다. 

도로 상태를 실시간으로 모니터링하고 손상된 구간을 자율주행 시스템에 미리 알림으로써 차량이 안전한 경로를 선택하거나 손상된 도로를 회피할 수 있도록 돕는다.

이를 통해 자율주행 차량의 안전성과 주행 효율성을 크게 향상시키며, 도로 관리 시스템과 자율주행 기술의 통합적인 발전에 기여한다. 

(Segmentation을 활용한 프로젝트)

<p align="center">
  <img src="https://thumbnews.nateimg.co.kr/view610///news.nateimg.co.kr/orgImg/ch/2020/09/28/2020092800213_0.jpg" width="700" />
</p>

--- 


# **프로젝트 개요**

도로의 차선 훼손은 빗물의 유입, 무거운 트럭 등이 지나감으로써 지반 자체가 약해져 발생한다.

특히 차선에 대한 차선 훼손의 발생은 운전자의 차선 인식에 불편함 제공 + 차선의 인식 문제로 인한 사고가 발생한다.

차선 훼손 문제를 해결하고자 현장에서 육안으로 조사하는 수동적 방법을 사용하기엔 매년 수 만개의 훼손이 발생하기 때문에 올바른 방법으로 선택하기엔 어렵다고 판단한다.

이러한 문제를 해결하고자 Yolov8(You Only Look Once) 기술을 활용해 데이터를 전처리한 후 이미지를 활용해 차선 훼손 검출 기술을 연구하고 실시간 탐지에 대한 정밀도, 실용성 등 검증 시도한다.

--- 


# **프로젝트의 배경** 

도로 차선의 훼손은 운전자와 차량에 큰 위험을 초래할 수 있으며, 이를 효과적으로 탐지하고 관리하는 것은 도로 유지 보수 및 자율주행을 관련하여 중요한 과제이다.

현재 다양한 차선 탐지 방법이 연구되고 있으며, 그 중 실시간으로 탐지가 가능한 시스템 개발이 주목받고 있다.

그러므로 촬영된 도로 이미지를 대상으로 전처리를 통해 차선의 훼손 정도 및 여부를 판단하여 처리할 수 있는 환경을 개발합니다. 

이 시스템은 객체 탐지에 강점을 가진 딥러닝 모델인 Yolov8 segmentation을 사용해, 주행 중 수집된 영상에서 도로의 차선 훼손 정도를 실시간으로 정밀하게 탐지하고, 해당 객체가 훼손된 차선인지 정상적인 도로 차선인지 판단하는 기능을 갖추게 한다.

---


# 도로 훼손 객체 탐지 알고리즘 설계

## 전처리 과정 및 순서

I. 데이터 수집

- 다양한 도로환경 영상 수집 (훼손된 도로, 정상 도로 모두 포함)

II. 데이터 정리 및 분류 

-  데이터 확인 후, 훼손된 객체 | 정상적인 객체 분류
-  최종적 데이터 : (1517장 사용) --- (훼손돈 객체 : 517개) --- (정상적인 객체 : 1000개)

III. 데이터 레이블링

- Label Studio를 활용하여 데이터 객체 라벨 부여
- 각 데이터에 대해 객체의 위치와 종류를 정확히 분류
- 데이터셋 구성 (훈련 8(1215) : 검증 1(151) : 테스트 1(151))

IV. 데이터 전처리 

- 이미지 크기 조정, 형식 변환으로 모델에 적합한 데이터로 변환
- (필요에 따라 데이터 증강으로 데이터 셋 보완 시도 가능)

V. 데이터 검증 및 저장

- 레이블링 및 전처리가 완료된 데이터 검증을 통해 오류나 누락 부분 확인
- 전처리 데이터를 학습용 데이터 셋으로 저장

---

# 모델 설명 및 설계 
https://docs.ultralytics.com/ko (Ultralytics 페이지)

**YOLO에는 Detect, Segment, Classify, Pose, OBB 등의 기술을 제공**

## YOLO (You Only Look Once) - Segmentation

<p align="center">
<img src="https://github.com/user-attachments/assets/a76bd8c6-6879-48ab-ae86-c87a77a886b2" width="700" height="400" />
</p>

## Segmentation 기술 선정 배경

**1. Detection과 다르게 Segmentation은 객체의 경계를 넘어 픽셀 단위로 훼손 영역과 정상 영역을 정확히 구분 가능** 

**2. 정확한 크기 및 위치, 작은 균열이나 구멍 등 감지에 용이함. -> 유지보수 작업에 세부적 데이터 제공 가능**

**3. 데이터 시각화 및 분석 용이, 색상별 분류를 통해 직관적으로 도로의 상태를 시각화 가능 -> 보수 필요 영역 판단**

**4. 클래스 별 Segmentation을 통해 정교한 구분 가능 -> 손상 정도에 따라 맞춤형 유지 보수 계획 수립 가능**

**5. 객체의 중복(중첩)을 처리 가능, 포괄적 도로 관리 가능**


