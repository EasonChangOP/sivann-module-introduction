# BLE Nine-Axis Sensor Module 
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware_Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service_&_Characteristic_UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann的 BLE Nine-Axis 模組有三軸數位的磁力感測器、三軸數位的加速度感測器以及三軸數位陀螺儀，其磁力、加速度以及陀螺儀三個感測器所感測的資訊皆可透過低功號藍芽 BLE 模組以無線方式讀取。模組有 MAG3110FCR1 以及 LSM6DS3 兩個感測器，前者用來感測磁力， 後者用來感測加速度及陀螺儀，詳細資訊附於文件最後的 Reference 章節 ，請自行參閱。

#### Features  
 * 讀取磁力、加速度和陀螺儀三軸數值  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 模組工作電壓: 3.3V (可使用 3V AA/CR2032 電池或 3.7V LiPo 鋰離子聚合物電池)  
 * 模組最大工作電流: 16mA  
 * 3軸陀螺儀，範圍 ±2000dps  
 * 3軸加速度，範圍 ±16g  
 * 3軸磁力計，範圍 ±1000uT  


<a name="Hardware_Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 模組以及底層電源模組(底層為鈕扣電池供電)，如下圖所示。  

![Nine-Axis](http://i.imgur.com/Bqg16jLl.png "Nine-Axis")  


<a name="Usage"></a>
## 3. Usage  

1. 如下圖所示，於模組背面金屬凹槽處置入CR2032水銀電池供電，請注意金屬殼為正極。  
![Battery](http://i.imgur.com/N79YOCmm.png "Battery")  


<a name="Service_&_Characteristic_UUID"></a>
## 4. Service & Characteristic UUID  

|  Service Name           |  Service ID  |  Characteristic ID  |  Description   |  Access Type  |  Note                                    |  
|-------------------------|--------------|---------------------|----------------|---------------|------------------------------------------|  
|  **Nine-Axis Service**  |   0xBB20     |  0xCC24             |  Gyro Data     |  R            |  X, Y, Z axis, Unit : dps                |  
|                         |              |  0xCC0F             |  Accel Data    |  R            |  X, Y, Z axis, Unit : mg                 |  
|                         |              |  0xCC10             |  Mag Data      |  R            |  X, Y, Z axis, Unit : uT                 |  
|                         |              |  0xBB21             |  9-Axis Conf.  |  R/W          |  0x01 (ON), 0x00 (OFF)                   |  
|                         |              |  0xBB22             |  9-Axis Peri.  |  R/W          |  Range 10~255, Period = [Input * 10] ms  |  
|  **DIN Service**        |   0xBB00     |  0xCC00             |  DIN Data      |  R            |  0x01 (H), 0x00 (L)                      |  
|  **AIN Service**        |   0xBB10     |  0xCC02             |  AIN Data      |  R            |  Unit : mV                               |  
|                         |              |  0xBB11             |  AIN Conf.     |  R/W          |  0x01 (ON), 0x00 (OFF)                   |  
|                         |              |  0xBB12             |  AIN Peri.     |  R/W          |  Range 10~255, Period = [Input * 10] ms  |  


<a name="Reference"></a>
## 5. Reference  

 * [MAG3110 Datasheets](https://www.nxp.com/files/sensors/doc/data_sheet/MAG3110.pdf "MAG3110")  
 * [LSM6DS3 Datasheets](http://www.st.com/content/ccc/resource/technical/document/datasheet/a3/f5/4f/ae/8e/44/41/d7/DM00133076.pdf/files/DM00133076.pdf/jcr:content/translations/en.DM00133076.pdf "LSM6DS3")  
 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/weatherStation.js "Nine-Axis Sample Code")  
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-nineaxis/blob/master/index.js "Nine-Axis Plugin")  