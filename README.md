# Human-Protein-Atlas-Competition-in-Kaggle

link : [https://www.kaggle.com/c/hpa-single-cell-image-classification](https://www.kaggle.com/c/hpa-single-cell-image-classification)<br>

안녕하세요. AiRLab(한밭대학교 인공지능 및 로보틱스 연구실) 노현철입니다.<br>

# Overview
저는 2021.02.01. ~ 2021.05.05. 까지 Kaggle에서 주최한 <Human Protein Atlas - Single Cell Classification> Competition에 참가하였습니다. <br>

이 Competition의 Overview는 단백질의 위치에 따라 작업하는 역할이 달라져 세포의 이질성이 유발된다고 합니다. 또한, 단백질은 모든 세포 과정에서 필수적인 역할을 하며, 다른 종류의 단백질들이 특정 위치에 모여 작업을 수행한다면 이 결과는 존재하는 단백질의 종류에 따라 다릅니다. 이러한 단백질들은 세포사이의 큰 이질성을 일으킬 수 있기 때문에 해당 세포의 단백질의 위치 정보와 종류를 알아낸다면 세포가 어떤 기능을 수행하는지, 질병이 어떻게 발생하는지, 더 나은 치료법을 개발하는 방법을 이해하는데 중요하게 생각하여 열린 Competition입니다.<br>
  
## Dataset
본 Competition의 데이터 셋의 이미지는 현미경에서 세포를 확대하고 촬영한 이미지이며 weak image-level labels로 되어 있습니다. 또한 각 이미지에는 여러 가지 cell이 존재하고, 각 cell 마다 라벨이 다를 수도 있기 때문에 multi-label로 라벨링이 되어있습니다. 최종 submission은 image-level이 아닌 cell-level 에서의 라벨을 필요로 합니다. <br>
  
<img src="https://user-images.githubusercontent.com/53032349/118927700-2653aa80-b97d-11eb-855a-6c758d00de4d.png" width="80%" height="80%" title="70px" alt="memoryblock"><br>
  
라벨은 총 19개로 구성되어 있으며, 의미는 다음과 같습니다.<br>
<img src="https://user-images.githubusercontent.com/53032349/118927833-5602b280-b97d-11eb-9973-b73b17dd885e.JPG" width="80%" height="80%" title="70px" alt="memoryblock"><br>
  
  
# Approach
<img src="https://user-images.githubusercontent.com/53032349/118927937-7c285280-b97d-11eb-81d1-14af4d86f20c.JPG" width="80%" height="80%" title="70px" alt="memoryblock"><br>
