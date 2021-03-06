# Human-Protein-Atlas-Competition-in-Kaggle

link : [https://www.kaggle.com/c/hpa-single-cell-image-classification](https://www.kaggle.com/c/hpa-single-cell-image-classification)<br>

안녕하세요. AiRLab(한밭대학교 인공지능 및 로보틱스 연구실) 노현철입니다.<br>
저는 2021.02.01. ~ 2021.05.05. 까지 Kaggle에서 주최한 **<Human Protein Atlas - Single Cell Classification>** Competition에 참가하였습니다. <br>
# Overview

이 Competition의 Overview는 단백질의 위치에 따라 작업하는 역할이 달라져 세포의 이질성이 유발된다고 합니다. 또한, 단백질은 모든 세포 과정에서 필수적인 역할을 하며, 다른 종류의 단백질들이 특정 위치에 모여 작업을 수행한다면 이 결과는 존재하는 단백질의 종류에 따라 다릅니다. 이러한 단백질들은 세포사이의 큰 이질성을 일으킬 수 있기 때문에 해당 세포의 단백질의 위치 정보와 종류를 알아낸다면 세포가 어떤 기능을 수행하는지, 질병이 어떻게 발생하는지, 더 나은 치료법을 개발하는 방법을 이해하는데 중요하게 생각하여 열린 Competition입니다.<br>
  
## Dataset
본 Competition의 데이터 셋의 이미지는 현미경에서 세포를 확대하고 촬영한 이미지이며 weak image-level labels로 되어 있습니다. 또한 각 이미지에는 여러 가지 cell이 존재하고, 각 cell 마다 라벨이 다를 수도 있기 때문에 multi-label로 라벨링이 되어있습니다. 최종 submission은 image-level이 아닌 cell-level 에서의 라벨을 필요로 합니다. <br>
  
<img src="https://user-images.githubusercontent.com/53032349/118927700-2653aa80-b97d-11eb-855a-6c758d00de4d.png" width="80%" height="80%" title="70px" alt="memoryblock"><br>
  
라벨은 총 19개로 구성되어 있으며, 의미는 다음과 같습니다.<br>
<img src="https://user-images.githubusercontent.com/53032349/118927833-5602b280-b97d-11eb-9973-b73b17dd885e.JPG" width="80%" height="80%" title="70px" alt="memoryblock"><br>
  
  
# Approach
<img src="https://user-images.githubusercontent.com/53032349/118927937-7c285280-b97d-11eb-81d1-14af4d86f20c.JPG" width="100%" height="100%" title="70px" alt="memoryblock"><br>
저의 접근방식은 다음과 같습니다. <br>

**1. Multi-label classification**<br>
**2. Cam**<br>
**3. Segment by cell**<br>
**4. Pseudo labeling**<br>
**5. Single-label classification**<br>


## Multi-label classification
<img src="https://user-images.githubusercontent.com/53032349/118978391-3c2f9280-b9b2-11eb-82aa-67ce09dcb764.png" width="100%" height="100%" title="70px" alt="memoryblock">
image-level label 에서 cell-level label 까지 도출해야 하기 때문에 우선적으로 기본 성능을 알아보고, 또한 어떠한 아이디어가 나오든 무조건 필요하다 생각하여 Multi-label classification을 진행하였습니다. 모델은 Resnet101, Efficientnet b3, b4, b5, b6, b7 로 진행하였었고 여러 가지 기법들도 적용하여 최종적으로 Resnet101 : 70.7%, Efficientnet b7 : 70.65%를 달성하였습니다. (해당 점수는 train set의 10%를 val set으로 사용하여 나타내었습니다.) <br>


## Cam

  
<img src="https://user-images.githubusercontent.com/53032349/118973382-94fc2c80-b9ac-11eb-9f4a-885ca86d7685.png" width="100%" height="100%" title="70px" alt="memoryblock"><br>
<img src="https://user-images.githubusercontent.com/53032349/118973819-105dde00-b9ad-11eb-9544-db2f20889d78.png" width="100%" height="100%" title="70px" alt="memoryblock"><br>
  
Cam은 Weakly supervised learning에서 자주 사용하는 기법이고, 본 대회측의 말에 의하면 한 이미지에 대한 multi-label이 존재하지만 이미지 안에 있는 여러 가지 cell에는 해당 라벨이 없을 수도 있다고 하였기 때문에 저는 각 label마다 cam을 찍어 각 라벨마다 어디를 보고 판단하는지 확인하는게 필요하다 생각하였습니다. (예시: image-label은 0,5,8이고 이미지 안에 a, b라는 cell이 존재할 때, cell-label이 각 각 a는 0,5,8, b는 8 일 수도 있다.)<br>

## Segment by cell
<img src="https://user-images.githubusercontent.com/53032349/118976732-4baddc00-b9b0-11eb-9206-54e78b8b6580.JPG" width="100%" height="100%" title="70px" alt="memoryblock"><br>
<img src="https://user-images.githubusercontent.com/53032349/118976764-57010780-b9b0-11eb-969a-5197a097c45a.JPG" width="100%" height="100%" title="70px" alt="memoryblock"><br>
이미지에 여러 가지 cell이 존재하기 때문에 이를 각각의 cell로 나눌 필요성을 느꼈고, 대회측에서도 무조건적으로 사용해야 하는 것이기 때문에 기본 cell segmentation tool을 제공해 주었습니다. 이 후에 submission에서 run time over가 나타났었고 이를 segmentation 하는 부분에서 시간을 많이 소모한다는 것을 발견했습니다. 저와 같은 이유로 제출이 안된다 하시는 분들을 검색해보았고 어떤 참가자의 fest cell segmentation tool 제공해주어 해결하였습니다.<br>

## Pseudo labeling
이미지당 cell의 개수가 적게는 5개미만, 많게는 100개 이상이였습니다. 우리는 앞서 진행한 cam과 cell segmentation을 가지고 pseudo labeling을 진행하였습니다. cam에서 나온 heatmap을 가지고 일정 수치 이상인 값들로 labeling, 그 외의 값을 가지는 cell은 새로운 class를 만들어 따로 저장하였습니다. 총 cell의 개수는 490,000개 정도였고 이중 labeling이 진행된 cell은 60,000개 정도였습니다. 총 cell의 개수에 비해 사용하는 cell이 너무 적다고 판단하여 나중에는 위에 있는 사이클을 한번 더 적용하여 80,000개 정도 까지 늘렸습니다. <br>

  
## Single-label classification
<img src="https://user-images.githubusercontent.com/53032349/118949736-80139f00-b994-11eb-8667-0737477fbea9.JPG" width="100%" height="100%" title="70px" alt="memoryblock"><br>
위에서 설명한 접근방식을 토대로 하여 최종적으로 cell-lavel pseudo label이 있는 데이터 셋을 완성하였고, 이를 Single-label classification 하였습니다. pre-train으로는 imagenet을 사용하려 했지만 테스크가 너무 다른 테스크였기 때문에 앞서 진행한 multi-label classification에서의 70.*%모델들을 사용하였습니다. 처음 사이클 한번 돌았을 때 성능은 **30 ~ 35%** 이였고, 위 사이클을 한 번 더 돌았을 때 최종적으로 **41.14%** 달성하였고 대회를 마쳤습니다.<br>

# Review
Kaggle이라는 곳에서 첫 번째로 진행하였던 대회였습니다. 처음이다보니 대회의 진행 순서, 방법, submission 하는 방법 등등 많은 고난과 역경이 있었습니다.(특히 submission...)<br>
그럼에도 불구하고, 옆에서 같이 도와주시던 연구원님, 랩실 형, 동기와 같이 이런 대회를 참가해 볼 수 있어서 좋은 기회였다고 생각합니다. 점수로는 도와주신것에 비해 못 나왔지만 최종적으로 41.14%를 달성하여 top 9%에서 마무리 하여 처음 대회 치고 괜찮다!! 위로하며 다음 대회에서는 좀더 좋은 성적을 거두기를 노력할겁니다! 감사합니다!!<br>
  
