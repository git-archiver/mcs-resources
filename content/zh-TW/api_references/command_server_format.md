# Command server 格式

此章節將會說明所有 command server 的格式，此格式為 command server 發送指令置裝置的格式。

**此處使用 UNIX timestamp 時間格式。

裝置會從 command server 接收到以下格式的指令，並且使用者可以自行寫一段解析程式來處理收到的指令。



## 事前準備

在裝置能接收 MCS 指令前，裝置須先和 MCS 平台做相連。


呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to 來取得一組 ip 位置以及連接阜來建立連結。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
來打開任意一個 tcp connection，並且傳送一個 heartbeat 訊息。

Heartbeat 格式:

```
    deviceId,deviceKey,timestamp

```

若您不希望在 heartbeat 中傳送實際的 timestamp，您可以直接在 timestamp 欄位輸入 0 為其值。

當 TCP 長連結建立後，您將可以開始使用 MCS 平台來對您的裝置下指令。

指令的形式如下：
```
    deviceId,deviceKey,timestamp,dataChnId,commandValue

```


## 各種資料通道的 command 格式


### 開關

```
deviceId,deviceKey,timestamp,dataChnId,{0 or 1}

```
0 代表關，1 代表開。

範例：

switch01,, 1

代表將 switch01 資料通道的狀態改為開，並且由系統自動帶入時間。

### 分類
```
deviceId,deviceKey,timestamp,dataChnId,{Key Value}
```
Key value 的值將會對應至您所設定的 Key name。

### 整數
```
deviceId,deviceKey,timestamp,dataChnId,{Integer}
```

### 浮點數
```
deviceId,deviceKey,timestamp,dataChnId,{Float}
```

### 十六進位數
```
deviceId,deviceKey,timestamp,dataChnId,{Hex value}
```
十六進位數的值為 A-F 以及 0-9。

### 字串
```
deviceId,deviceKey,timestamp,dataChnId,{string}
```

### GPS
```
deviceId,deviceKey,timestamp,dataChnId,{latitude},{longitude},{altitude}
```

緯度範圍從 -90 至 90。 0 至 90 代表北緯，0 至 -90 代表南緯。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 0 至 20000 公尺。

### GPIO
```
deviceId,deviceKey,timestamp,dataChnId,{0 ot 1}
```
0 代表低，1 代表高。

### PWM
```
deviceId,deviceKey,timestamp,dataChnId,{value},{period}

```

### 類比
```
deviceId,deviceKey,timestamp,dataChnId,{value}

```

### 遊戲控制器
```
deviceId,deviceKey,timestamp,dataChnId,{up/down/right/left/A/B value|press(1) or release(0)}
```

### 圖片
```
deviceId,deviceKey,timestamp,dataChnId,{image file base64 encoding string value}
```
