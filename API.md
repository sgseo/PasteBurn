# PasteBurn API

[TOC]

## 登录（login）

### 基本信息

地址：https://skywt.cn/paste/api/login.php
方法：POST

### 请求参数

|参数名|类型|必须|默认值|说明|
|------|----|----|------|----|
|user|字符串|True|/|用户名|
|pswd|字符串|True|/|密码|

### 返回数据

返回数据为 json 格式。

|名称|类型|说明|
|----|----|----|
|success|逻辑型|是否成功|
|info|字符串|如果失败返回错误信息，如果成功则为空|
|token|字符串|如果成功返回用户 token，如果失败则为空|

注意：**取得的用户 token 24 小时之内有效。**

## 推送文本（push）

### 基本信息

地址：https://skywt.cn/paste/api/push.php
方法：POST

### 请求参数

|参数名|类型|必须|默认值|说明|
|------|----|----|------|----|
|text|字符串|True|/|需要推送的文字，不能为空|
|token|字符串|False|/|用户 token，如不发送则不记录用户|
|savetime|逻辑型|False|`false`|是否记录存储时间|

### 返回数据

返回数据为 json 格式。

|名称|类型|说明|
|----|----|----|
|success|逻辑型|是否成功|
|info|字符串|如果失败返回错误信息，如果成功则为该文本的 uid|

## 取回文本并焚毁（get）

### 基本信息

地址：https://skywt.cn/paste/api/get.php
方法：GET

### 请求参数

|参数名|类型|必须|默认值|说明|
|------|----|----|------|----|
|uid|字符串|True|/|文本的 uid|

### 返回数据

返回数据为 json 格式。

|名称|类型|说明|
|----|----|----|
|success|逻辑型|是否成功|
|info|字符串|如果失败返回错误信息，如果成功则为空|
|text|字符串|如果成功返回文本内容，如果失败则为空|
|user|字符串|如果成功且有用户则返回用户名，否则为空|
|time|字符串|如果成功且存储时记录了时间则返回时间，否则为空|

注意：**取出文本后文本会立即焚毁，再次查询将失败。**

注意：返回文本中对 `&`、`"`、`'`、`<`、`>` 字符进行了转义，需要自行恢复。转义表参见文末。
php 可以使用 `htmlspecialchars_decode()` 函数；
jQuery 可参见：[jQuery 两句话实现 HTML 转义与反转义](https://www.cnblogs.com/woostundy/p/4138173.html)

## 字符转义表

|字符|名称|转义为|
|----|----|------|
|`&`|和号|`&amp;`|
|`"`|双引号|`&quot;`|
|`'`|单引号|`&#039;`|
|`<`|小于号|`&lt;`|
|`>`|大于号|`&gt;`|