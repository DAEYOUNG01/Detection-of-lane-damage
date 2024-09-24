# 도로 손상 객체 검출 시스템(Detection_of_lane_damage)
---


# CONTENTS


* **프로젝트 제목** : 프로젝트의 간략한 이름 및 설명

  
* **프로젝트 개요** : 프로젝트에 대한 전반적인 설명(배경, 목적, 제안 이유)

  
* **도로 훼손 객체 탐지 알고리즘 설계** : 알고리즘 설계에 대한 내용


* **데이터 세트 및 모델 설명**

  
* **프로젝트 결과**


* **프로젝트의 한계 및 향후 연구 방향**


* **기대효과** 
---


## 프로젝트 제목 : SegRoad

SegRoad는 도로 이미지에서 손상된 부분을 정확하게 검출하기 위한 세그멘테이션 기반 시스템입니다. 

이를 통해 도로 유지보수 효율성을 높이고, 안전한 주행 환경을 제공합니다.

SegRoad는 자율주행 차량을 위한 중요한 데이터 소스로 활용될 수 있습니다. 

도로 상태를 실시간으로 모니터링하고 손상된 구간을 자율주행 시스템에 미리 알림으로써 차량이 안전한 경로를 선택하거나 손상된 도로를 회피할 수 있도록 돕습니다. 

이를 통해 자율주행 차량의 안전성과 주행 효율성을 크게 향상시키며, 도로 관리 시스템과 자율주행 기술의 통합적인 발전에 기여합니다. (Segmentation)
![image](https://thumbnews.nateimg.co.kr/view610///news.nateimg.co.kr/orgImg/ch/2020/09/28/2020092800213_0.jpg)


## **프로젝트 개요**

도로의 차선 훼손은 빗물의 유입, 무거운 트럭 등이 지나감으로써 지반 자체가 약해져 발생합니다.

특히 차선에 대한 차선 훼손의 발생은 운전자의 차선 인식에 불편함을 제공하며, 차선의 인식 문제로 인한 사고가 발생할 수 있습니다. 

차선 훼손 문제를 해결하고자 현장에서 육안으로 조사하는 수동적 방법을 사용하기엔 매년 수 만개의 훼손이 발생하기 때문에 어려움이 발생할 수 있습니다. 

이러한 문제를 해결하고자 Yolov8(You Only Look Once) 기술을 활용해 데이터를 전처리한 후 이미지를 활용해 차선 훼손 검출 기술을 연구하고 실시간 탐지에 대한 정밀도, 실용성 등을 검증합니다.


