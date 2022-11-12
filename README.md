<img src="https://user-images.githubusercontent.com/52292818/201135464-26b73133-5855-48a9-b3bd-3c8c867bde04.png" width="500px">

## Introduction
파이썬 개발자를 위한 종 분포 모델링(SDM: Species Distribution Modeling)을 구현합니다. SDM은 컴퓨터 알고리즘을 사용하여 지리적 시공간에 걸쳐 종의 분포를 예측하는 모델링입니다. SDM for Python Developers의 소스코드는 2020년 미국 데이터사이언티스트 다니엘 퍼먼(Daniel Furman)이 공개한 [[A brief introduction to Species Distribution Models in Python]](https://daniel-furman.github.io/Python-species-distribution-modeling/) 오픈소스를 기반으로 합니다. 국립공원공단 지리공간분석가 유병혁은 2021년 다니엘 퍼먼의 일부 소스코드를 최적화해서 [[QGIS와 Python을 이용한 종 분포 모델링(SDM)]](https://www.youtube.com/watch?v=UpUmAVvnL04) 유튜브 콘텐츠 등으로 재공유했습니다. 이후 [[2022년 데이터 청년 캠퍼스]](https://www.lafent.com/inews/news_view.html?news_id=131228&wrter=%EC%9C%A0%EB%B3%91%ED%98%81+%EA%B3%BC%EC%9E%A5) 빅리더 AI 아카데미 프로젝트에 참여한 공희배, 전영웅, 이은주, 김진규, 김민기 5명의 데이터과학 전공자가 소스코드를 PoC(Proof of Concept) 단계의 소프트웨어 WAY(Where Are You)로 발전시켰습니다. SDM for Python Developers는 유병혁에 의해 개발 중이며 경상국립대학교 조경학과 대학원(이수동 교수)에서 테스터로 참여하며 배포되고 있습니다.

* 개발자
  * 유병혁 (국립공원공단 사회가치혁신실 <bhyu@knps.or.kr>; OSGeo Charter Member; [GGRS](https://foss4g.tistory.com/) 기술블로거)
  * 공희배 (경남대학교 전자공학과)
  * 전영웅 (동서울대학교 소프트웨어학과)
  * 이은주 (단국대학교 수학과; 컴퓨터공학과)
  * 김진규 (경남대학교 경제금융학과; 빅데이터AI학과)
  * 김민기 (서울과학기술대학교 컴퓨터공학과)
  * 배진익 (PT Mobility Doctor Indonesia)
  
* 테스터
  * 이수동, 김현, 박경식, 오충현, 조봉교, 진민화 (경상국립대학교 조경학과 대학원)
  * 안미연 (부산대학교 조경학과 대학원)
  * 윤성수 (국립생태원 생태정보팀)
  * 성정모 (국립공원공단 속리산국립공원사무소)

## Prerequisites
내 컴퓨터에 [Python(파이썬)](https://www.python.org/)을 설치합니다.  
웹프라우저에서 파이썬 프로그래밍이 가능한 'Jupyter Notebook(주피터 노트북)'도 설치합니다.
```
pip install jupyter notebook
```
SDM for Python Developers, aka SDM4PyDev 구동을 위한 의존성 패키지는 다음과 같습니다. 설치를 진행합니다.
```
pip install gdal
pip install pyproj
pip install six
pip install rtree
pip install shapely
pip install fiona
pip install rasterio
pip install pandas
pip install geopandas
pip install numpy
pip install matplotlib
pip install xgboost
pip install lightgbm
pip install pyimpute
```
일부 의존성 패키지가 설치되지 않는 경우 pipwin 패키지를 통해 설치합니다.
```
pip install --upgrade pip
pip install wheel
pip install pipwin
pipwin refresh
```
## Try SDM4PyDev!
* 클라우드 기반에서 SDM4PyDev를 구동해 보실 수 있습니다. [[SDM4PyDev on Google Colab]](https://colab.research.google.com/drive/1Mo1GuM6BnKKquHUYJiL1V0ZHhXNCQ42c?usp=sharing)은 국립공원 학습동아리 '파크랩(ParkLab)' 모임에 참여한 배진익 님이 자발적으로 제공해 주셨습니다.
<table>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/52292818/201135200-6d64b899-7b81-4984-b7bd-534deb698ddf.png" width="500"></td>
    <td><img src="https://user-images.githubusercontent.com/52292818/201136500-3b487284-a885-4b79-ba11-00cd9251a8b8.png" width="500"></td>
  <tr>
</table>

* 경상국립대학교 조경학과 김현 연구원님은 물두꺼비(Korean toad; Bufo stejnegeri) 연구에 SDM4PyDev를 활용하고 계십니다.
<table>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/52292818/201481405-d627880c-b96d-4858-b6c3-5fb12774b49e.jpg" width="500"></td>
    <td><img src="https://user-images.githubusercontent.com/52292818/201481406-09ead698-abf3-47cf-acba-7b580ef32464.jpg" width="500"></td>
  <tr>
</table>

## Data
* BIOCLIM 폴더: 한반도 영역(33°∼43°N, 124°∼132°E)의 1970~2000년 평균 19종 생물기후 변수(Bioclimatic variables) [[데이터 출처]](https://www.worldclim.org/data/bioclim.html)
* Zosterops_japonicus.gpkg: 동박새(Warbling white-eye) 출현(presence) 좌표 [[데이터 출처]](https://plugins.qgis.org/plugins/qgisgbifapi/)
* ADM_KOR.gpkg: 행정구역 시군구 경계 [[데이터 출처]](http://data.nsdi.go.kr/dataset/20180927ds0058)

## SDM4PyDev Functions
* 출현 지점과 중복되지 않은 영역에서 임의 비출현 지점(pseudo-absence points)을 자동 생성합니다.
* 출현/비출현 지점에 대한 생물기후 변수 피처를 포인트 샘플링합니다.
* 8종 머신러닝(Machine Learning) 분류기를 지원합니다.
```
CLASS_MAP = {
    'RF': (RandomForestClassifier()), # 랜덤포레스트
    'ET': (ExtraTreesClassifier()), # 엑스트라트리
    'ADA' : (AdaBoostClassifier()), # 아다부스트
    'BAG' : (BaggingClassifier()), # 배깅
    'GRA' : (GradientBoostingClassifier()), # 그레디언트부스팅
    'XGB': (XGBClassifier()), # 엑스지부스트
    'LGBM': (LGBMClassifier()), # 라이트그레디언트부스팅
    'Maxent':(LogisticRegression()), # 로지스틱회귀(맥센트)
    }
```
