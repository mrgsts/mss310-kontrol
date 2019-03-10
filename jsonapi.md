## Details of the JSON API Request to control the MSS310 module

- The JSON query has an series of common params, **messageId, sign, timestamp**

   **messageId** is a string formed by a md5 of some random data
   
   **sign** this is the most important value, as my module validate every request with a sign value and do not provide response without valid data
   
   **timestamp** is a string contain the unix time

You can get your key and other useful values from my forked version of @bapirex [login.py](https://github.com/mrgsts/meross-api/blob/master/login.py)

Edit and run python login.py
```
userId: 291733
key: 03d06e1b24b386dfdb422249bc867a90
token: 7a07ede5c1915ff66c727de2821fad82896eb6a95b9896c7747238b97ba98396
messageId: 8b41bde6fca9558de1fa8cf64701da70
sign: b0da0c3d3cf57aa5d97696f59bdd8f81
timestamp: 1552218808
(Example data, no valid values)
```

- Example :

   If you key value is: 3fe8496944c2236b1b6edc8ea29dc8d5, a correct request values will be:

```
messageID: d052cd2e1f1d4bd4d76f5f2d93820dce
timestamp: 1552215950
sign: ef57aef6267c6990d23931ef6c64b871 (md5 of messageID + key + timestamp)
```

# HTTP JSON API Requests

You can use any HTTP client of your election, i use curl for the examples

- **Example of HTTP Query with curl**
```
curl --http1.1 --header "Content-Type: application/json"   --request POST   --data '{"header":{"from":"","messageId":"**********","method":"GET","namespace":"Appliance.System.All","payloadVersion":1,"sign":"**********","timestamp":1551966308},"payload":{}}'   http://<YOURMODULEIP>/config
```
- **Get All module config values**

   Curl "GET","namespace":Appliance.System.All"

*Response data*
```json
{"header":{"messageId":"**********","namespace":"Appliance.System.All","method":"GETACK","payloadVersion":1,"from":"/appliance/**********/publish","timestamp":1552217703,"timestampMs":195,"sign":"*********"},"payload":{"all":{"system":{"hardware":{"type":"mss310","subType":"us","version":"2.0.0","chipType":"mt7682","uuid":"**********","macAddress":"AA:BB:CC:DD:EE:FF"},"firmware":{"version":"2.1.9","compileTime":"2018/12/18 17:16:47 GMT +08:00","wifiMac":"AA:BB:CC:DD:EE:FF","innerIp":"192.168.100.10","server":"iot.meross.com","port":2001,"userId":"******"},"time":{"timestamp":1552217703,"timezone":"Europe/Madrid","timeRule":[[1540688400,3600,0],[1553994000,7200,1],[1572138000,3600,0],[1585443600,7200,1],[1603587600,3600,0],[1616893200,7200,1],[1635642000,3600,0],[1648342800,7200,1],[1667091600,3600,0],[1679792400,7200,1],[1698541200,3600,0],[1711846800,7200,1],[1729990800,3600,0],[1743296400,7200,1],[1761440400,3600,0],[1774746000,7200,1],[1792890000,3600,0],[1806195600,7200,1],[1824944400,3600,0],[1837645200,7200,1]]},"online":{"status":1}},"digest":{"togglex":[{"channel":0,"onoff":0,"lmTime":1552176889}],"triggerx":[],"timerx":[]}}}}

```

- **Set module MQTT config** if you have setup your MQTT custom server before, look at [mqtt-config.md](mqtt-config.md)

   Curl "SET","namespace":"Appliance.Config.Key"

*Payload data*
```json
{ "key": { "gateway": { "host": "192.100.100.1", "port": 8883, "secondHost": "192.100.100.1", "secondPort": "8883"}, "key": "**********", "userId": "******" }}
```
