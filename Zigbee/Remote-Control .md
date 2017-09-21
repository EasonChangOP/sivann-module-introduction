# BLE Remote Control Module
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware_Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service_&_Characteristic_UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Remote Control 模組上面有 5 個按鍵，每個按鍵的點擊都會透過 BLE 將資訊傳出，得知哪個按鍵被按下。  

#### Features  
 * 5 個按鍵給使用者使用  
 * 待機低耗電，點擊任一按鍵可觸發 BLE 廣播入網  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 模組工作電壓: 可使用 3V AA/CR2032 電池或 3.7V LiPo 鋰離子聚合物電池  
 * 模組最大工作電流: 20mA   
 * 按鍵點擊前/後電壓（3.3V / 0V）  


<a name="Hardware_Overview"></a>
## 2. Hardware Overview  

此無線模組為三種模組堆疊而成，包括上層感測模組、中層 BLE 模組以及底層電源模組，如下圖所示。  

![RemoteControl](http://i.imgur.com/eqWtOzp.png "RemoteControl")  


<a name="Usage"></a>
## 3. Usage  

1. 如下圖所示，於模組背面金屬凹槽處置入 CR2032 水銀電池供電，請注意**金屬殼為正極** 
![Battery](http://i.imgur.com/vHfVrlW.png "Battery")  

2. 點擊任意按鍵，綠色 LED 開始閃爍，模組發出 BLE 廣播加入網路  


<a name="Service_&_Characteristic_UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |  Char. Name           |  Char. ID  |  Possible Fields in Char. Value               |  Access Type  |  Unit  |  Description                                         |  
|----------------|--------------|-----------------------|------------|-----------------------------------------------|---------------|--------|------------------------------------------------------|  
|  **Key**       |   0xBB70     |  Multistate Selector  |  0xCC32    |  id (uint8), flags (uint8), mStateIn (uint8)  |  R            |        |  1 (UP), 2 (DOWN), 4 (SELECT), 8 (LEFT), 16 (RIGHT)  |  


<a name="Reference"></a>
## 5. Reference  

 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/remoteControl.js "Remote Control Sample Code")  
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-remotecontrol/blob/master/index.js "Remote Control Plugin")  
