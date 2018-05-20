Raspberry Pi側実装のWorkspace

## 役割分担  
1. LEDライトの点灯  
  led.pyにkick_lighting関数を実装  
  引数: 色, 点灯秒数  
  戻り値: なし  

2. 周囲にあるbluetoothデバイスを検知  
  other_device.pyにdetect関数を実装  
  引数: なし  
  戻り値: デバイスのリスト  

3. オーケストレーター
通信プロトコルに則り、bluetoothのシリアル通信をしてしてライトの点灯をキック/近接デバイス情報のアップロードを行う
  
# 通信プロトコル  
bluetoothを介してシリアル通信を行う　　
シリアル通信はjsonで行う

LEDライト点灯はiOSアプリが以下のようなjsonをrasberry piに向かって送る
(赤色LEDを１秒間点灯させる)
```LEDライトの点灯用のjson  
{"action":"led","time":1,"color":"red"}
```

すれ違い情報の送信は以下のようなjsonをrasberry piからiOSアプリに向かって送る
```周囲にid1及びid2のデバイスがいる場合
{"action":"near-device","devices":["id1","id2"]}
```
