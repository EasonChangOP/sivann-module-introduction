# BLE Remote Control Module
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service & Characteristic UUID)  


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
## 3. Service & Characteristic UUID  

|        Service Name & ID             |  Characteristic Description  |  Characteristic ID  |  Value                                                             |  Description               |  
|--------------------------------------|------------------------------|---------------------|--------------------------------------------------------------------|----------------------------|  
|  *Key Service (0xBB70)*              |  Key Data (R)                |  0xCC32             |  0x01 (UP), 0x02 (DOWN), 0x04 (SELECT), 0x08 (LEFT), 0x10 (RIGHT)  |  Key Status                |  
|  *DIN Service (0xBB00)*              |  DIN Data (R)                |  0xCC00             |  0x01 (H), 0x00 (L)                                                |  DIN Status                |  
|  *AIN Service (0xBB10)*              |  AIN Data (R)                |  0xCC02             |  00:00 (mV)                                                        |  LSB:MSB                   |  
|                                      |  AIN Conf. (R/W)             |  0xBB11             |  0x01 (ON), 0x00 (OFF)                                             |  Measurement               |  
|                                      |  AIN Peri. (R/W)             |  0xBB12             |  0x0A (10) ~ 0xFF (255)                                            |  Period = [Input * 10] ms  |  
