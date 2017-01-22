# BLE Gas Alarm Sensor Module 
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service & Characteristic UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Gas Alarm 模組內建一組 MQ-2 氣體感測器以及警報用蜂鳴器，煙霧濃度數值及蜂鳴器的開關可透過低功號藍芽 BLE 模組以無線方式讀取及控制。MQ-2 感測器對於煙、甲烷、丙烷和乙醇等氣體有不同的敏感度，而其量測氣體的預設為煙霧。MQ-2 詳細資料請參閱 Reference 的連結。  

#### Features  
 * 讀取煙霧濃度與其他可燃性氣體，單位 ppm  
 * 自動警報功能 : 濃度 > 300ppm (Defalut)，Defalut 可手動調整  
 * 透過 BLE 遠端操作蜂鳴器開關、設置不同氣體種類的敏感度以及觸發蜂鳴器的濃度值  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 模組工作電壓：5V  
 * 模組最大工作電流：240mA  
 * 模組可感測煙霧濃度範圍：300 - 10000ppm (300ppm 以下為估算值，其最低值為 100 ppm)  
 * MQ-2 預熱時間：48 hours  


<a name="Hardware Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![GasAlarm](http://i.imgur.com/hUozm7i.png "GasAlarm")  


<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB 以 5V 電源供應  
2. 等待煙霧感測器 MQ-2 預熱完畢後，可開始正常量測  

#### Note  
1. 自動警報功能需預熱 10 分鐘後 (一次性)，才會自動啟用。  
2. 每次重新啟動須預熱 15 秒，模組才會開始量測。  
3. MQ-2 感測器的特性需預熱一段時間，數值才較準確。  


<a name="Service & Characteristic UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name            |  Service ID  |  Char. Name          |  Char. ID  |  Possible Fields in Char. Value                                                       |  Access Type  |  Unit  |  Description                                       |  
|--------------------------|--------------|----------------------|------------|---------------------------------------------------------------------------------------|---------------|--------|----------------------------------------------------|  
|  **Environmental**       |   0xBB50     |  Generic             |  0xCC04    |  id (uint8), flags (uint8), sensorValue (float), units (string), sensorType (string)  |  R            |  ppm   |  Gas Measurment Data                               |  
|                          |              |  GasAlarm Conf.      |  0xBB51    |  config (boolean)                                                                     |  R/W          |        |  Measurment Switch. 0 (OFF), 1 (ON)                |  
|                          |              |  GasAlarm Peri.      |  0xBB52    |  period (uint8)                                                                       |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255      |  
|                          |              |  GasAlarm Option     |  0xBB53    |  option (uint8)                                                                       |  R/W          |        |  0 (Propane), 1 (Smoke), 2 (Methane), 3 (Ethanol)  |  
|                          |              |  GasAlarm Threshold  |  0xBB54    |  threshold (uint16)                                                                   |  R/W          |  ppm   |  Gas Alarm Limit Range : 100~10000 ppm             |  
|  **Buzzer**              |   0xBB60     |  Buzzer              |  0xCC28    |  id (uint8), flags (uint8), onOff (boolean), minOffTime (float)                       |  R/W          |        |  0 (OFF), 1 (ON)                                   |  
|  **DIN**                 |   0xBB00     |  Digital Input       |  0xCC00    |  id (uint8), flags (uint8), dInState (boolean)                                        |  R            |        |  0 (Low), 1 (High)                                 |  
|  **AIN**                 |   0xBB10     |  Analogue Input      |  0xCC02    |  id (uint8), flags (uint8), aInCurrValue (float), sensorType (string)                 |  R            |  mV    |                                                    |  
|                          |              |  AIN Conf.           |  0xBB11    |  config (boolean)                                                                     |  R/W          |        |  Measurment Switch. 0 (OFF), 1 (ON)                |  
|                          |              |  AIN Peri.           |  0xBB12    |  period (uint8)                                                                       |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255      |  


<a name="Reference"></a>
## 5. Reference  

 * [MQ-2 Datasheets](http://www.buyic.com.tw/datasheet/0113004018/data.rar "MQ-2")  
 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/gasAlarm.js "Gas Alarm Sample Code")  
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-gassensor/blob/master/index.js "Gas Alarm Plugin")  
