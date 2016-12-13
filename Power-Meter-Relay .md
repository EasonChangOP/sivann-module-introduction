# BLE Power Meter Relay Module  
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service & Characteristic UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Power Meter Relay 模組有繼電器當開關以及電流感測器，可以透過低功號藍牙 BLE 透過無線方式控制切換電器開關和讀取量測的電流值。電流感測器 (ACS712ELCTR-05B-T) 以及繼電器 (TRB1-05D) 的相關詳細資料在 Reference，請自行參閱。  

#### Features  
 * 量測 AC/DC 電流，電流值最大不超過 3A  
 * 控制繼電器 NC/NO  
 * 綠色LED提示繼電器切換至 NO  
 * 支援 2.4GHz BLE 4.0，並符合 BIPSO 規範  

#### Spec  
 * 模組工作電壓: 5V  
 * 模組最大工作電流: 85mA  
 * 繼電器壽命: 100,000 次 (電子式切換)  
 * 繼電器規格: 3A, 120VAC / 24VDC  
 * 控制繼電器 NC/NO  


<a name="Hardware Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![Smart Power Relay](http://i.imgur.com/P35N7FNl.png "Smart Power Relay")  

#### Pinouts  

![Smart Power Relay Top Module](http://i.imgur.com/GWADze7m.png "Smart Power Relay Top Module")  

* Power Pins:  
  * 5V – 5V 的電源腳位。供電給繼電器及 ACS712 使用  
  * Vcc (3.3V) – 3.3V 的電源腳位。供電給光耦合器  
  * GND – 模組地參考平面   
* AO  
  讀取 ACS712 的電流量測資訊  
* DIN  
  控制繼電器 NO/NC ，繼電器的 NO/NC 對應於 DIN 的電壓 0V/3.3V  
* 5VCal  
  參考電壓，數值為 5V 的一半  
* PIR (optional)  
  讀取 PIR 人體紅外線感測器的觸發狀態 (0V/3.3V)。這是選擇性的腳位，使用者可以藉由此腳位來讀取觸發狀態，並與其它應用做結合  


<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB 以 5V 電源供應  
2. 連接電器，如下圖所示  


<a name="Service & Characteristic UUID"></a>
## 4. Service & Characteristic UUID  

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |  Char. Name       |  Char. ID  |  Access Type  |  Unit  |  Description                                   |  
|----------------|--------------|-------------------|------------|---------------|--------|------------------------------------------------|  
|  **Meter**     |   0xBB30     |  Power            |  0xCC1E    |  R            |  W     |                                                |  
|                |              |  Current          |  0xCC13    |  R            |  A     |                                                |  
|                |              |  P & C Conf.      |  0xBB31    |  R/W          |        |  Meter Measurment. 0(OFF), 1(ON)               |  
|                |              |  P & C Peri.      |  0xBB32    |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255  |  
|  **Relay**     |   0xBB40     |  Power Control    |  0xCC0E    |  R/W          |        |  0(OFF), 1(ON)                                 |  
|  **PIR**       |   0xBB90     |  Presence Sensor  |  0xCC06    |  R/W          |        |  0(L), 1(H)                                    |  
|  **DIN**       |   0xBB00     |  Digital Input    |  0xCC00    |  R            |        |  0(L), 1(H)                                    |  
|  **AIN**       |   0xBB10     |  Analogue Input   |  0xCC02    |  R            |  mV    |                                                |  
|                |              |  AIN Conf.        |  0xBB11    |  R/W          |        |  aIn Measurment. 0(OFF), 1(ON)                 |  
|                |              |  AIN Peri.        |  0xBB12    |  R/W          |        |  Period = [Data * 10] ms, Data Range : 10~255  |  



<a name="Reference"></a>
## 5. Reference  

* Sensor  
  [ACS712 Datasheets](http://pdf1.alldatasheet.com/datasheet-pdf/view/168326/ALLEGRO/ACS712.html "ACS712")  

* Sample Code(ble-shepherd)  

* Plugin (ble-shepherd)  
  [Power Meter Relay](https://github.com/bluetoother/bshep-plugin-sivann-relay/blob/master/index.js "Power Meter Relay")  
