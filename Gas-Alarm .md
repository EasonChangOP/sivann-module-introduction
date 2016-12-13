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

sivann 的 BLE Gas Alarm 模組內建一組 MQ2 氣體感測器以及警報用蜂鳴器，煙霧濃度數值及蜂鳴器的開關皆可透過低功號藍芽 BLE 模組以無線方式讀取及控制。MQ2 元件本身對煙、甲烷、丙烷和乙醇等氣體有不同的敏感度，而 sivann 氣體感測器的讀取值的對照參數為煙霧。詳細資料可參考 Reference 章節。  

#### Features  
 * 讀取煙霧濃度與其他可燃性氣體，單位 ppm  
 * 煙霧濃度超過 300ppm 後會自動觸發 Buzzer，發出蜂鳴警報  
 * 可透過 BLE 以無線方式控制，獨立操作蜂鳴器開關  

#### Spec  
 * 模組工作電壓：5V  
 * 模組最大工作電流：240mA  
 * 模組可感測煙霧濃度範圍：300 - 2000ppm (300ppm 以下為估算值)  
 * MQ2 預熱時間：48 hours  


<a name="Hardware Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![GasAlarm](http://i.imgur.com/b48dpg1l.png "GasAlarm")  

### Pinouts  
![GasAlarm Top](http://i.imgur.com/AMoCMcBm.png "GasAlarm Top")  

* Power Pins:  
  * 5V –5V的電源腳位。供電給 MQ-2 使用  
  * Vcc (3.3V) –3.3V 的電源腳位。供電給 Buzzer  
  * GND – 模組地參考平面  
* AO  
  氣體濃度 (MQ-2) 的電壓輸出  
* Alarm_EN  
  控制 Buzzer 鳴叫  

<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB以5V電源供應  
2. 待煙霧感測器 MQ2 預熱完畢後，可開始正常量測  


<a name="Service & Characteristic UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service                 |  Service ID  |  Char. Name          |  Char. ID  |  Access Type  |  Uint  |  Description                                       |  
|--------------------------|--------------|----------------------|------------|---------------|--------|----------------------------------------------------|  
|  **Environmental**       |   0xBB50     |  Generic             |  0xCC04    |  R            |  ppm   |  Gas Data                                          |  
|                          |              |  GasAlarm Conf.      |  0xBB51    |  R/W          |        |  1(ON), 0(OFF)                                     |  
|                          |              |  GasAlarm Peri.      |  0xBB52    |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255      |  
|                          |              |  GasAlarm Option     |  0xBB53    |  R/W          |        |  0(Propane), 1(Smoke), 2(Methane), 3(Ethanol)      |  
|                          |              |  GasAlarm Threshold  |  0xBB54    |  R/W          |        |  Gas Alarm Limit Range : 10~10000                  |  
|  **Buzzer**              |   0xBB60     |  Buzzer              |  0xCC28    |  R/W          |        |  Buzzer Data; 1(ON), 0(OFF)                        |  
|  **DIN**                 |   0xBB00     |  Digital Input       |  0xCC00    |  R            |        |  DIN Data; 1 (H), 0 (L)                            |  
|  **AIN**                 |   0xBB10     |  Analogue Input      |  0xCC02    |  R            |  mV    |  AIN Data                                          |  
|                          |              |  AIN Conf.           |  0xBB11    |  R/W          |        |  1(ON), 0(OFF)                                     |  
|                          |              |  AIN Peri.           |  0xBB12    |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255      |  


<a name="Reference"></a>
## 5. Reference  

#### Sensor  
[LM358 Datasheets](http://www.ti.com/lit/ds/symlink/lm358.pdf "LM358")  
[MQ2 Datasheets](http://www.buyic.com.tw/datasheet/0113004018/data.rar "MQ2")  


#### Sample Code(ble-shepherd)  


#### Plugin (ble-shepherd)  

[Gas Alarm](https://github.com/bluetoother/bshep-plugin-sivann-gassensor/blob/master/index.js "Gas Alarm")  
