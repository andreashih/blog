---
title: DOCX Files Search and Manipulation
description: 這學期 (108-2) 修大學部的 python 課程，在期末用 python-docx 搭配 python 內建函式庫做了一個迷你專案。
date: 2020-06-29
slug: 
image: books3.jpg
categories:
    - coding
tags:
    - python
---


這學期 (108-2) 修大學部的 python 課程，在期末用 [**<u>python-docx</u>**](https://python-docx.readthedocs.io/en/latest/) 搭配 python 內建函式庫做了一個[**<u>迷你專案</u>**](https://github.com/andreashih/docx-search-manipulation)。

最初的想法如下圖：

{{< figure src="python_docx.png" title="專案發想" width="60%" height="auto">}}


## Code
---

```python
import os
import os.path
from os import path
import docx
from docx import Document
import re
import shutil
from shutil import copyfile
```

使用者輸入原資料夾所在的路徑。若路徑存在則將 working directory 設為使用者輸入的路徑，若路徑不存在則印出警告訊息。

```python
path1 = '123'
while path.exists(path1) == False:
    path1 = input('Please enter the location of the original files:')  
    if path.exists(path1):
        os.chdir(path1) # Set working directory
    else:
        print('Warning: Invalid path')
```
  
使用者輸入關鍵字（可接受 regular expression），並將含有其關鍵字的 .docx 檔案存到 `matched_files` 中，再做出各個含有關鍵字檔案的路徑，存到 `matched_files_paths`。

```python
# A function that extracts files that match the pattern
def search_file(filename, pattern):
    doc = docx.Document(filename)
    text = []
    for para in doc.paragraphs:
        text.append(para.text)
    if re.findall(pattern, str(text)) != []:
        return filename
    else:
        return 0
```

```python
# Search docx files with content matching particular pattern
pattern = input('Please enter the keyword')
matched_files = []
for file in os.listdir():
    if not file.endswith('.docx'): continue
    x = search_file(file, pattern)
    if x != 0:
        matched_files.append(x)
```    

```python
# Extract matched files path
matched_files_paths = []
for matched_file in matched_files:
    path = f"{path1}\\{matched_file}"
    matched_files_paths.append(path)
```

有了 `matched_files_paths`，就可以對含有關鍵字的 .docx 檔案進行操作。使用者可以輸入 `move` 或 `copy`，再輸入新路徑（欲移動或複製至哪一個資料夾），或是直接輸入 `delete`，將含有關鍵字的 .docx 檔案刪除。

```python
# A function that manipulates files (move, copy, or delete)
def file_manipulate(mode, matched_file_path, to):
    if mode == 'move':
        shutil.move(matched_file_path, to)
    elif mode == 'copy':
        shutil.copy(matched_file_path, to)
    elif mode == 'delete':
        os.remove(matched_file_path)        
    else:
        return 'no such mode'
```

```python
mode = '123'
while mode not in ['move','copy', 'delete']:
    mode = input('move, copy, or delete?')
    if mode == 'delete':
        to = ''
        for matched_file_path in matched_files_paths:
                file_manipulate(mode, matched_file_path, to)  
    elif mode in ['move', 'copy']:
        to = input("Please provide the new file path")
        if path.exists(to) == False:
            print('Warning: Invalid path')
        else:
            for matched_file_path in matched_files_paths:
                file_manipulate(mode, matched_file_path, to)
    else:
        print('Warning: Invalid mode')
```

&nbsp;

## Murmuring
---

真心覺得對初學者來說，盡量不要同時學兩個程式。資質駑鈍如我無法同時參透兩個語言，因此這學期就是不斷把 R 寫在 python 裡或把 python 寫在 R 裡。寫完一整天的 python 要再回去寫 R，簡直像濃霧中漫步伸手不見五指。順攝抑制和倒攝抑制在我身上嶄露無遺。所以學程式不要貪快貪多，會消化不良（倘若列位看官是程式小天才則另當別論）。像這個簡單的小專案就讓我做了超級久（從適應 python 語法到寫出好像可以 run 的東西），而且還不大完善。最好的方式就是早一點開始學，不要像我一樣 code 到用時方恨少！

&nbsp;

## 參考資料
---
[**<u>Search all docx files with python-docx in a directory (batch)</u>**](https://stackoverflow.com/questions/42682648/search-all-docx-files-with-python-docx-in-a-directory-batch)

[**<u>Searching docx Files in python</u>**](https://stackoverflow.com/questions/22819948/searching-docx-files-in-python)

[**<u>How to use regular expressions with python docx?</u>**](https://stackoverflow.com/questions/60682266/how-to-use-regular-expressions-with-python-docx)

[**<u>How to Create, Move, and Delete Files in Python</u>**](https://stackabuse.com/how-to-create-move-and-delete-files-in-python/)

&nbsp;

<span>Photo by <a href="https://unsplash.com/@inakihxz?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Iñaki del Olmo</a> on <a href="https://unsplash.com/s/photos/library?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>