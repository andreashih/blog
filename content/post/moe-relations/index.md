---
title: 查詢萌典中的同義詞和反義詞
description: 萌典是一部由臺灣開源社群 - g0v 零時政府開發的數位化漢語詞典。
date: 2022-04-11
slug: 
image: book-shadow.jpg
categories:
    - coding
tags:
    - python
    - crawler
---

## 關於萌典
---
萌典是一部由臺灣開源社群 [**<u>g0v 零時政府</u>**](https://github.com/g0v)開發的數位化漢語詞典。國語資料來源為《教育部重編國語辭典修訂本》，閩南語資料來自《臺灣閩南語常用詞辭典》，客家語資料則源自《臺灣客家語常用詞辭典》。除此之外，該計畫近日也新增了[**<u>阿美語萌典</u>**](https://amis.moedict.tw/)。
- [**<u>網站</u>**](https://www.moedict.tw)
- [**<u>GitHub</u>**](https://github.com/g0v/moedict-webkit)

&nbsp;

## 方法一： BeautifulSoup
---

```python
import requests
from bs4 import BeautifulSoup
```

以「容忍」一詞為例：

```python
word = '容忍'

res = requests.get(url = f'https://www.moedict.tw/{word}')
print(res)

## <Response [200]>
```

確認請求成功後，回到網頁，使用快捷鍵 `Option+Command+U`（Windows: `Ctrl + U`，或是右鍵 -> View Page Source），從網頁原始碼中可以看到同義詞和反義詞藏在 \<span> tag 裡面。

```python
soup = BeautifulSoup(res.text, 'lxml')
span_syn = soup.select('span.synonyms')
span_ant = soup.select('span.antonyms')

if span_syn:
  syn = span_syn[0].get_text()
  syns = syn[1:].split('、')
else: syns = []

if span_ant:
  ant = span_ant[0].get_text()
  ants = ant[1:].split('、')
else: ants = []

moe_relations = {'synonyms': syns, 'antonyms': ants}
```

最後得到「容忍」的同義詞和反義詞如下：

```python
moe_relations

## {'antonyms': ['發作', '拒絕', '生氣'], 'synonyms': ['忍耐']}
```

&nbsp;

## 方法二： urllib
---

```python
import urllib.request, urllib.parse
import json
```

同樣以「容忍」一詞為例：

```python
word = '容忍'
word_urllib = urllib.parse.quote_plus(word)

with urllib.request.urlopen(f'https://www.moedict.tw/raw/{word_urllib}') as url:
    data = json.loads(url.read().decode())
```

將 `json` 檔讀進來，結構如下：

```python
data

## {'heteronyms': [{'bopomofo': 'ㄖㄨㄥˊ ㄖㄣˇ',
##    'bopomofo2': 'rúng rěn',
##    'definitions': [{'antonyms': '發作,拒絕,生氣',
##      'def': '包容、忍耐。',
##      'quote': ['漢書．卷八十六．王嘉傳：「唯陛下留神於擇賢，記善忘過，容忍臣子，勿責以備。」',
##       '元．無名氏．連環計．第四折：「倒是呂布兄弟還容忍得過，若我白袍李肅呵，殺了那老賊多時也。」'],
##      'synonyms': '忍耐'}],
##    'pinyin': 'róng rěn'}],
##  'title': '容忍'}
```

從 `json` 檔中一層一層抓出同義詞和反義詞：

```python
syns = data.get('heteronyms')[0].get('definitions')[0].get('synonyms')
ants = data.get('heteronyms')[0].get('definitions')[0].get('antonyms')

if syns:
  syns = syns.split(',')
else: syns = []

if ants:
  ants = ants.split(',')
else: ants = []

moe_relations = {'synonyms': syns, 'antonyms': ants}
```
最後結果如下：

```python
moe_relations

## {'antonyms': ['發作', '拒絕', '生氣'], 'synonyms': ['忍耐']}
```

&nbsp;

## 結論
---
相較於以語意關係為主軸建置的[**<u>中文詞彙網路</u>**](https://lopentu.github.io/CwnWeb/)，萌典的語意關係資料較少，僅部分詞條具有同義及反義詞，且並未區分同義和近義。但萌典收錄的詞條較為完整，還有讀音、部首、筆劃等資訊，可以用於不同研究主題。

👩‍💻 本文程式碼[***<u>連結</u>***](https://github.com/andreashih/semantic_relations/blob/main/moe_relations.ipynb)

&nbsp;

Photo by <a href="https://unsplash.com/@richasharma96?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Richa Sharma</a> on <a href="https://unsplash.com/s/photos/book?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
