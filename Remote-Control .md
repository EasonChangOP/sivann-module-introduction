# BLE Remote Control Module
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service & Characteristic UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Remote Control 模組上面有5個按鍵，每個按鍵的點擊都會透過 BLE 將資訊傳出，得知哪個按鍵被按下。  

#### Features  
 * 5 個按鍵給使用者使用  
 * 待機低耗電，點擊任一按鍵可觸發 BLE 廣播入網  
 * 支援 2.4GHz BLE 4.0，並符合 BIPSO 規範  

#### Spec  
 * 模組工作電壓: 可使用 3V AA/CR2032 電池或 3.7V LiPo 鋰離子聚合物電池  
 * 模組最大工作電流: 20mA   
 * 按鍵點擊前/後電壓（3.3V / 0V）  


<a name="Hardware Overview"></a>
## 2. Hardware Overview  

此無線模組為三種模組堆疊而成，包括上層感測模組、中層 BLE 模組以及底層電源模組，如下圖所示。  

![RemoteControl](http://i.imgur.com/PxBDAJQl.png "RemoteControl")  

### Pinouts  
![RemoteControl Top Module](http://i.imgur.com/vEMSWk2m.png "RemoteControl Top Module")  

* Power Pins:  
  * Vcc(3.3V) – 3.3V 電源腳位  
  * GND – 模組地參考平面  
* Button – (點擊按鍵前/後的電壓 Vcc/0V)  
  * Right – 右按鍵  
  * Left – 左按鍵  
  * Up – 上按鍵  
  * Down – 下按鍵  
  * OK – 中心按鍵  


<a name="Usage"></a>
## 3. Usage  

1. 如下圖所示，於模組背面金屬凹槽處置入CR2032水銀電池供電，請注意金屬殼為正極  
![Battery](http://i.imgur.com/N79YOCmm.png "Battery")  

2. 點擊任意按鍵，綠色LED開始閃爍，模組發出BLE廣播加入網路  


<a name="Service & Characteristic UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |  Char. Name           |  Char. ID  |  Access Type  |  Unit  |  Description                                         |  
|----------------|--------------|-----------------------|------------|---------------|--------|------------------------------------------------------|  
|  **Key**       |   0xBB70     |  Multistate Selector  |  0xCC32    |  R            |        |  1 (UP), 2 (DOWN), 4 (SELECT), 8 (LEFT), 16 (RIGHT)  |  
|  **DIN**       |   0xBB00     |  Digital Input        |  0xCC00    |  R            |        |  0 (L), 1 (H)                                        |  
|  **AIN**       |   0xBB10     |  Analogue Input       |  0xCC02    |  R            |  mV    |                                                      |  
|                |              |  AIN Conf.            |  0xBB11    |  R/W          |        |  aIn Measurment. 0 (OFF), 1 (ON)                     |  
|                |              |  AIN Peri.            |  0xBB12    |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255        |  

<a name="Reference"></a>
## 5. Reference  

*  Sample Code(ble-shepherd)  


*  Plugin (ble-shepherd)  
   [Remote Control](https://github.com/bluetoother/bshep-plugin-sivann-remotecontrol/blob/master/index.js "Remote Control")  
