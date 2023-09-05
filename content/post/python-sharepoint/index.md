---
title: 使用 Python 取得 Microsoft Sharepoint 的資料
description: 需要的資料都在 Sharepoint，但是一個一個下載太花時間了。
date: 2023-09-05
slug: 
image: laptop.jpg
categories:
    - coding
tags:
    - python
---

[Microsoft Sharepoint](https://support.microsoft.com/zh-tw/office/%E4%BB%80%E9%BA%BC%E6%98%AF-sharepoint-97b915e6-651b-43b2-827d-fb25777f446f) 是許多公司內部分享資料的平台。我們有時會需要從 Sharepoint 上取得大量資料，但是一個一個點擊下載會花很多時間。本文將介紹如何用 Python 將 Microsoft Sharepoint 的資料更快速自動地下載到本機。

## 下載並載入套件
```python
!pip install python-dotenv
!pip install Office365-REST-Python-Client
!pip install git+https://github.com/vgrem/Office365-REST-Python-Client.git
```
```python
# For office365 library
from office365.runtime.auth.authentication_context import AuthenticationContext
from office365.sharepoint.client_context import ClientContext
from office365.sharepoint.files.file import File 
# For .env file
import os
from dotenv import load_dotenv
load_dotenv()
```

## 連上 Sharepoint
為了安全可以將資訊另存在 `.env` 中，但要注意不要不小心上傳到 Git。
```python
SHAREPOINT_BASE_URL = # Sharepoint 連結
SHAREPOINT_USER = # 帳號
SHAREPOINT_PASSWORD = # 密碼
```
接著就可以使用 `os.getenv()` 取得 `.env` 中的參數。
```python
sharepoint_base_url = os.getenv("SHAREPOINT_BASE_URL")
sharepoint_user = os.getenv("SHAREPOINT_USER")
sharepoint_password =  os.getenv("SHAREPOINT_PASSWORD")
```
連接到 Sharepoint。
```python
auth = AuthenticationContext(sharepoint_base_url)
auth.acquire_token_for_user(sharepoint_user, sharepoint_password)
ctx = ClientContext(sharepoint_base_url, auth)
web = ctx.web
ctx.load(web)
ctx.execute_query()
print('Connected to SharePoint: ',web.properties['Title'])
```
<pre>
Connected to SharePoint:  My Sharepoint
</pre>

## 下載檔案
設定資料夾路徑。
```python
sharepoint_folder = # Sharepoint 資料夾路徑
output_dir = # 檔案儲存於本機的路徑
if not os.path.exists(output_dir):
    os.mkdir(output_dir)
```
列出資料夾下的檔案名稱。
```python
folder = ctx.web.get_folder_by_server_relative_url(sharepoint_folder)
filenames = []
sub_folders = folder.files 
ctx.load(sub_folders)
ctx.execute_query()
for s_folder in sub_folders:
    filenames.append(s_folder.properties["Name"])
```
下載檔案到本機。
```python
for filename in filenames:
    path = os.path.join(sharepoint_folder, filename)
    file_response = File.open_binary(ctx, path)
    if file_response.content:
        with open(os.path.join(output_dir, filename), 'wb') as output_file:  
            output_file.write(file_response.content)
        print(f"{filename} saved")
```
<pre>
001.txt saved
002.txt saved
fig.png saved
</pre>

這樣就完成了！

&nbsp;

## 參考資料

1. https://stackoverflow.com/questions/59979467/accessing-microsoft-sharepoint-files-and-data-using-python  
1. https://github.com/bashamsc/sharepoint_python/blob/main/sharepoint_read_file_python.py

&nbsp;

Photo by <a href="https://unsplash.com/@windows?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Windows</a> on <a href="https://unsplash.com/photos/C6T6vr1sQI0?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>