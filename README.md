# SDM for Python Developers

## Introduction
파이썬 개발자를 위한 __종 분포 모델링(SDM: Species Distribution Modeling)__을 구현합니다. 소스코드는 미국 데이터사이언티스트 다니엘 퍼먼(Daniel Furman)이 공개한 [[A brief introduction to Species Distribution Models in Python]](https://daniel-furman.github.io/Python-species-distribution-modeling/) 오픈소스를 기반으로 합니다. 다니엘 퍼먼의 소스코드는 국립공원공단 지리공간분석가 유병혁에 의해 업데이트되어 [[2011년 QGIS와 Python을 이용한 종 분포 모델링(SDM)]](https://www.youtube.com/watch?v=UpUmAVvnL04) 유튜브 콘텐츠 등으로 재공유되었습니다. 이후 [[2022년 데이터 청년 캠퍼스]](https://www.lafent.com/inews/news_view.html?news_id=131228&wrter=%EC%9C%A0%EB%B3%91%ED%98%81+%EA%B3%BC%EC%9E%A5) 프로젝트를 통해 공희배, 전영웅, 이은주, 김진규, 김민기 5명에 의해 소스코드는 발전되었습니다. SDM for Python Developers는 프로젝트 종료 이후에 유병혁에 의해 재정리된 것입니다.

* 개발자
  * 유병혁 (국립공원공단 사회가치혁신실; OSGeo Foundation Charter Member)
  * 공희배 (경남대학교 전자공학과)
  * 전영웅 (동서울대학교 소프트웨어학과)
  * 이은주 (단국대학교 수학과; 컴퓨터공학과)
  * 김진규 (경남대학교 경제금융학과; 빅데이터AI학과)
  * 김민기 (서울과학기술대학교 컴퓨터공학과)
  
* 테스터
  * 이수동, 김현, 박경식, 오충현, 조봉교, 진민화 (경상국립대학교 조경학과)
  * 안미연 (부산대학교 조경학과)

## Prerequisites
SDM for Python Developers 구동을 위한 의존성 패키지는 다음과 같습니다.
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
