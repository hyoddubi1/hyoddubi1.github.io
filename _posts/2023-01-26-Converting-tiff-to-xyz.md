---
layout: post
title: Converting tiff (.tif) raster file to ascii xyz (.xyz)
subtitle: Osgeo, gdal gdal2xyz
categories: Python
tags: [Python, osgeo, gdal]
---

### Using QGIS

QGIS는 `공간 처리 툴박스-GDAL-래스터 변환-gdal2xyz` 경로로 접근하면 레이어에 떠있는 래스터를 대상으로 변환할 수 있다.

또는 `Processing toolbox / GDAL/OGR / [GDAL] Conversion / gdal2xyz`

그런데 이상하게 결과 파일이 생성되지 않았다.
아래 로그를 첨부한다.
```
알고리즘 처리 중...
'gdal2xyz' 알고리즘 시작…
Input parameters:
{ 'BAND' : 1, 'CSV' : False, 'INPUT' : 'D:/directory/dtm.tif', 'OUTPUT' : 'D:\output directory\output_dtm.txt' }

GDAL command:
python3 -m gdal2xyz -band 1 "D:\tiff directory\target_dtm.tif"  "D:\output directory\output_dtm.txt"
GDAL command output:
C:\PROGRA~1\QGIS3~1.10\bin\python3.exe: No module named gdal2xyz

Execution completed in 0.96 seconds
Results:
{'OUTPUT': 'D:\output directory\output_dtm.txt'}

출력 레이어 불러오기
Algorithm 'gdal2xyz' finished
```

보니까 중요한 건 `No module named gdal2xyz`인 것 같다. 아무래도 QGIS 상에서 작동하는 Python 환경에 gdal2xyz라는 모듈 혹은 패키지가 없어서 나타나는 것 같다. QGIS에서는 깔려 있는데 가상환경 상에서 지원이 안 되는 것 같다. 그래서 QGIS를 별도로 깔기는 좀 무리가 있어서 파이썬 자체에서 작동해보기로 했다.


### Using gdal2xyz.py in Python environment (Anaconda environment)

우선 준비물은 `gdal`이 있는 `osgeo` 패키지이다.
QGIS 로그에 보면 `python3 -m gdal2xyz -band 1 "D:/directory/dtm.tif"`라고 돼 있는데, 아무래도 QGIS가 파이썬 스크립트를 터미널에서 실행시키는 놈이 저 모양인 것 같다.
그래서 `osgeo`가 설치된 가상환경을 `conda activate 가상환경`로 실행시키고 아래처럼 하니 성공적으로 추출됐다.
```
python C:\Users\user\anaconda3\envs\geoanal\Scripts\gdal2xyz.py -band 1 "D:\tiff directory\target_dtm.tif" "D:\output directory\output_dtm.txt"
```

그리고 프로세싱 정도를 `0...10...20...`처럼 보여준다.




