# 取得与特定版本相容的固件列表

## 描述

使用 **HTTPs GET** 来从 MCS 取得与特定版本相容的固件列表。


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/available/:versionId

```
此 API 在版本相容性的查询上提供了更弹性的作法，可直接查询与指定版本相容的固件列表。


### 查詢參數
可將下列參數帶入請求 URL  

| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| url | 字串 | 布林值 | 非必要的参数。加上 **url=true** 后，伺服器将会回传各固件的下载网址|

## 动作
HTTPs GET


## 参数
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### 回覆格式
回覆格式為 JSON

## 回覆

### 回覆代码
200

### 回覆 Header
JSON 格式
```
Content-Type:`application/json`
```

### 回覆內容

***JSON 格式：***

JSON 格式的回覆内容会包含以下几个栏位：

|栏位名称|格式|描述|
| --- | --- | --- | --- |
| results | array | 所有与特定版本相容的固件列表，可参考 **/firmware/available** API |
|code| string|http 状态代码|
|message|string|系统讯息|


**范例：**

请求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/available/1
```

请求 Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`


回覆內容

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "results": [
        {
            "fwid": "FAdJBknrDsOM",
            "name": "hello firmware",
            "description": null,
            "version": "2"
        },
        {
            "fwid": "Fwnx3ZBxOLCK",
            "name": "firmware_2",
            "description": null,
            "version": "3"
        }
    ]
}

```


## 错误回覆

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下资讯：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| message | String | 错误描述 |

**范例：**

```
{
    "apiVersion": "2.8.0",
    "code": 401,
    "message": "401 Unauthorized",
    "errors": [
        {
            "code": 401,
            "message": "401 Unauthorized"
        }
    ],
    "results": "you dont have permission!",
    "statusCode": 401,
    "options": {}
}
```


