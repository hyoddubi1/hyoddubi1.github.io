---
layout: post
title: Pandas SettingWithCopyWarning or SettingWithCopyError 해결법
subtitle: Pandas DataFrame copy 문제
categories: Python
tags: [Python, pandas]
---

### 문제의 에러 메시지

```
__main__:1: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
```


```python
import numpy as np
import pandas as pd

gps = pd.read_csv("D:/gps.csv")

y1 = gps[gps.name.str.contains('Y1')]

y1['Y2'] = y1['Y'].values

```

요런 코드에서 오류가 났다.

찾아보니 copy warning인데 지정된 DataFrame을 딥카피하면 해결된다고 한다.

위 코드같은 경우에는 `gps`변수의 index를 이용해 `y1` 변수가 선언돼있는데, 이렇게 바로 지정하면 y1변수가 gps의 메모리 위치를 참조해버리기 때문인 것 같다.

이런 경우에 `y1`은 그냥 gps의 저 선언된 위치를 보여주는거라서

gps의 메모리를 공유하는 `y1`을 수정코자 하니까 gps를 수정해야하나? 하는 생각을 하는 것 같다.

이런 경우 Deep copy를 해야 하는데 간단히 뒤에 `.copy()`를 해주면 된다.

그러면 컴퓨터가 해당 변수의 '정보'들을 복사해서 새로운 메모리를 할당해주니까 꼬이지 않는다.

위 코드는 아래같이 바꾸면 된다.


```python
import numpy as np
import pandas as pd

gps = pd.read_csv("D:/gps.csv")

y1 = gps[gps.name.str.contains('Y1')].copy()

y1['Y2'] = y1['Y'].values

```