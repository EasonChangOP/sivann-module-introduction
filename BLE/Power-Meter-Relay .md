# BLE Power Meter Relay Module  
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware_Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service_&_Characteristic_UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Power Meter Relay 模組有繼電器、電流感測器以及人體紅外線感測器 ( PIR，為選擇性)，可以透過低功號藍牙 BLE 無線方式控制切換電器開關、讀取量測的電流值和 PIR 變化。電流感測器 (ACS712ELCTR-05B-T) 的詳細資料請參閱 Reference 的連結。  

#### Features  
 * 量測 AC 電流，電流值範圍 120 mA 至 3A (誤差範圍 10%)  
 * 量測 AC 功率，功率範圍 13 W 至 330 W (誤差範圍 10%)  
 * 控制繼電器 NC/NO  
 * 綠色 LED 提示繼電器切換至 NO  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 模組工作電壓: 5V  
 * 模組最大工作電流: 85mA  
 * 繼電器壽命: 100,000 次 (電子式切換)  
 * 繼電器規格: 3A, 120VAC / 24VDC  
 * 控制繼電器 NC/NO  


<a name="Hardware_Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![Smart Power Relay](http://i.imgur.com/HtcpIQ0.png "Smart Power Relay")  


<a name="Usage"></a>
## 3. Usage  

1. 連接電器  
2. 連接 Micro USB 以 5V 電源供應  
3. Optional - 可外接 PIR  

![Relay With PIR](http://i.imgur.com/lJygRXB.png "Relay With PIR")  


<a name="Service_&_Characteristic_UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |  Char. Name       |  Char. ID  |  Possible Fields in Char. Value                                        |  Access Type  |  Unit  |  Description                                   |  
|----------------|--------------|-------------------|------------|------------------------------------------------------------------------|---------------|--------|------------------------------------------------|  
|  **Metering**  |   0xBB30     |  Power            |  0xCC1E    |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  W     |                                                |  
|                |              |  Current          |  0xCC13    |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  A     |                                                |  
|                |              |  Metering Conf.   |  0xBB31    |  config (boolean)                                                      |  R/W          |        |  Measurment Switch. 0 (OFF), 1 (ON)            |  
|                |              |  Metering Peri.   |  0xBB32    |  period (uint8)                                                        |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255  |  
|  **Relay**     |   0xBB40     |  Power Control    |  0xCC0E    |  id (uint8), flags (uint8), onOff (boolean)                            |  R/W          |        |  0 (NC), 1 (NO)                                |  
|  **PIR**       |   0xBB90     |  Presence Sensor  |  0xCC06    |  id (uint8), flags (uint8), dInState (boolean), sensorType (string)    |  R/W          |        |  0 (Low), 1 (High)                             |  
|  **DIN**       |   0xBB00     |  Digital Input    |  0xCC00    |  id (uint8), flags (uint8), dInState (boolean)                         |  R            |        |  0 (Low), 1 (High)                             |  
|  **AIN**       |   0xBB10     |  Analogue Input   |  0xCC02    |  id (uint8), flags (uint8), aInCurrValue (float), sensorType (string)  |  R            |  mV    |                                                |  
|                |              |  AIN Conf.        |  0xBB11    |  config (boolean)                                                      |  R/W          |        |  Measurment Switch. 0 (OFF), 1 (ON)            |  
|                |              |  AIN Peri.        |  0xBB12    |  period (uint8)                                                        |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255  |  


<a name="Reference"></a>
## 5. Reference  

 * [ACS712 Datasheets](http://pdf1.alldatasheet.com/datasheet-pdf/view/168326/ALLEGRO/ACS712.html "ACS712")  
 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/powerMeterRelay.js "Power Meter Relay Sample Code")  
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-relay/blob/master/index.js "Power Meter Relay Plugin")  
