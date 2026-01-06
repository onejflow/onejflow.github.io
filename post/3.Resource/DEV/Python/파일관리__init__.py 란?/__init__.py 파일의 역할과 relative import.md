---
title: "[주제] 제목"
date: 2020-05-09T14:46:47+08:00
lastmod: 
draft: true
slug: 
categories: 
tags: 
math: true
mathJax: true
mermaid: true
toc: true
pin: false
summary: 요약글 작성 처음에 보이는거임..
---
# \__init__.py  파일의 역할

(출처-임커밋)
패키지를 구성하는 모듈들의 집합을 관리하기 위함

예시
models란 디렉토리에 
 - A.py 
 - B.py
 - C.py
 라고 각각 스크립트가 있고 class들이 있다면,
 main.py 에서
```python
# main.py
import models.A
import models.B
import models.C

model = models.A.A()
```
이런식으로 불러들여 사용할 수 있음

다른 방법으로는 아래와 같이 models.py 에 클래스들을 모아두고 할 수 있지만 모델이 추가될수록 코드 가독성이 안좋아짐
```python
# models.py
class A:
	def __init__(self):
		...

class B:
	def __init__(self):
		..
```

이런 상황을 해결하기 위한 방법

import models는 한번만 하고 각 모델이 분리된 파일에 있으면서 
model = models.A() 처럼 하려면?

folder/\_init__.py 를 하면됨![](Screenshot%202025-08-16%20at%2014.03.16.png)

이렇게 하면 models 라는 모듈(폴더)는 A,B,C를 가지고 있음
그래서 import models로 임포트 하면 가능

# relative import

각 폴더가 패키지라고 하면, relative import는 패키지안으로 제한되어 있다.

data/dataA.py 와 dataB.py는 상대경로에 따른 import 가 가능하지만 model 디렉토리는 상대경로에 따른 임포트 불가
```python
# dataB.py
from . import dataA
from model import modelA
```

![](Screenshot%202025-08-16%20at%2014.06.41.png)

- 현재 디렉토리  
    prj/  
    data/  
    dataA.py  
    dataB.py  
    model/  
    modelA.py
    
- data, model 폴더는 “패키지”여야 함 → 각각에 **init**.py 파일이 있어야 함.
- 실행은 프로젝트 루트(prj)에서 “모듈 실행” 형태로: python -m data.dataB
    
기본 답
- dataB.py에서 같은 패키지(data) 안의 dataA.py는 상대 임포트로  
    - from . import dataA
    - 또는: from .dataA import 함수명, 클래스명
    
- 다른 패키지(model)의 modelA.py는 형제 패키지이므로  
    - from model import modelA
    - 또는: from model.modelA import 함수명, 클래스명