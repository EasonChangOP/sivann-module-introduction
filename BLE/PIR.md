
# BLE PIR Module  
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware_Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service_&_Characteristic_UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE PIR 人體紅外線感測器模組，可以透過低功號藍牙 BLE 無線方式接收感測器訊號。電流感測器 (ACS712ELCTR-05B-T) 的詳細資料請參閱 Reference 的連結。  

#### Features  
 * 偵測人體紅外線  
 * 紅色 LED 顯示紅外線訊號  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 模組工作電壓：5V  
 * PIR 模組 OUT 腳位電壓輸出：3.3V / 0V  


<a name="Hardware_Overview"></a>
## 2. Hardware Overview  

此無線感測模組為兩種電路模組加上 PIR 感測器堆疊而成，有 BLE 無線模組，以及底層電源模組，如下圖所示。  

![PIR](http://i.imgur.com/HtcpIQ0.png "PIR")  


<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB 以 5V 電源供應  

![PIR](http://i.imgur.com/lJygRXB.png "PIR")  


<a name="Service_&_Characteristic_UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |  Char. Name       |  Char. ID  |  Possible Fields in Char. Value                                        |  Access Type  |  Unit  |  Description                                   |  
|----------------|--------------|-------------------|------------|------------------------------------------------------------------------|---------------|--------|------------------------------------------------|  
|  **PIR**       |   0xBB90     |  Presence Sensor  |  0xCC06    |  id (uint8), flags (uint8), dInState (boolean), sensorType (string)    |  R/W          |        |  0 (Low), 1 (High)                             |  
|  **AIN**       |   0xBB10     |  Analogue Input   |  0xCC02    |  id (uint8), flags (uint8), aInCurrValue (float), sensorType (string)  |  R            |  mV    |                                                |  
|                |              |  AIN Conf.        |  0xBB11    |  config (boolean)                                                      |  R/W          |        |  Measurment Switch. 0 (OFF), 1 (ON)            |  
|                |              |  AIN Peri.        |  0xBB12    |  period (uint8)                                                        |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255  |  


<a name="Reference"></a>
## 5. Reference  

 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/powerMeterRelay.js "PIR Sample Code")  
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-relay/blob/master/index.js "PIR Plugin")  
