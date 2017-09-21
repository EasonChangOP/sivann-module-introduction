# BLE Weather Station Module 
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware_Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service_&_Characteristic_UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Weather Station 模組有光度、壓力、溫度、濕度、聲音以及空氣的塵埃 (選擇性，需自己購買 PM 2.5/PM10 加裝) 的感測器，模組上感測器的數值皆透過低功號藍牙 BLE 無線方式傳出。光度感測器 (Si1132)、壓力感測器 (LPS25HB)、溫溼度感測器 (SHT20) 和麥克風 (SPW2430HR5H)，其相關的詳細資料請參閱 Reference 的連結。  

#### Features  
 * 量測環境光度 (Ambient light) 和 UVI  
 * 量測大氣壓力  
 * 量測溫度、溼度  
 * 量測聲音的變化  
 * 量測空氣塵埃 (Optional。連接 Grove Dust Sensor - DSM501A)  
 * 資料格式符合 [BIPSO](https://github.com/bluetoother/bipso/wiki/BIPSO-Specification "BIPSO") 規範  

#### Spec  
 * 環境光度 (Ambient light ) ：0 – 128k lux  
 * 大氣壓力：260 – 1260 hPa (海拔約 1875 – 10100 m)  
 * 分貝計範圍：35 – 80 dB  
 * 透過 SHT20 量測溫度和濕度  
 
 
<a name="Hardware_Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![WeatherStation](http://i.imgur.com/YvZv45R.png "WeatherStation")  


<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB 以 5V 電源供應  
2. Optional - 可連接 Grove Dust Sensor  


<a name="Service_&_Characteristic_UUID"></a>
## 4. Service & Characteristic UUID

下表為此模組的 Service 跟 Characteristic 的介紹，之後的 Characteristic 簡稱為 Char.。  

|  Service Name  |  Service ID  |   Char. Name     |  Char. ID (Handle ID\*)  |  Possible Fields in Char. Value                                        |  Access Type  |  Unit        |  Description                                         |  
|----------------|--------------|------------------|--------------------------|------------------------------------------------------------------------|---------------|--------------|------------------------------------------------------|  
|  **Weather**   |   0xBB80     |  Barometer       |  0xCC11                  |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  hPa         |                                                      |  
|                |              |  Temperature     |  0xCC07                  |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  °C          |                                                      |  
|                |              |  Humidity        |  0xCC08                  |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  %RH         |                                                      |  
|                |              |  Illuminance     |  0xCC05 (65)             |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  UV Index    |  UVI Data.                                           |  
|                |              |  Illuminance     |  0xCC05 (69)             |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  lux         |  Lux Data.                                           |  
|                |              |  Loudness        |  0xCC1A                  |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  dB-SBL      |                                                      |  
|                |              |  Concentration   |  0xCC1B                  |  id (uint8), flags (uint8), sensorValue (float), units (string)        |  R            |  pcs/0.01cf  |                                                      |  
|                |              |  Weather Conf.   |  0xBB81                  |  config (boolean)                                                      |  R/W          |              |  Measurment Switch. 0 (OFF), 1 (ON)                  |  
|                |              |  Weather Peri.   |  0xBB82                  |  period (uint8)                                                        |  R/W          |              |  Period = [Data * 10] ms, Data Range : 100~255       |  
|  **DIN**       |   0xBB00     |  Digital Input   |  0xCC00                  |  id (uint8), flags (uint8), dInState (boolean)                         |  R            |              |  0 (Low), 1 (High)                                   |  
|  **AIN**       |   0xBB10     |  Analogue Input  |  0xCC02                  |  id (uint8), flags (uint8), aInCurrValue (float), sensorType (string)  |  R            |  mV          |                                                      |  
|                |              |  AIN Conf.       |  0xBB11                  |  config (boolean)                                                      |  R/W          |              |  Measurment Switch. 0 (OFF), 1 (ON)                  |  
|                |              |  AIN Peri.       |  0xBB12                  |  period (uint8)                                                        |  R/W          |              |  Period = [Data * 10] ms, Data Range : 10~255        |  

\* : Handle ID 可用來分辨有同樣的 Char. ID 的資料。可參考 Reference 的 Sample Code 是如何處理有相同 Char. ID 的情況。  


<a name="Reference"></a>
## 5. Reference   

 * [LM358 Datasheets](http://www.ti.com/lit/ds/symlink/lm358.pdf "LM358")  
 * [Si1132 Datasheets](https://www.silabs.com/Support%20Documents/TechnicalDocs/Si1132.pdf "Si1132")  
 * [SHT20 Datasheets](https://www.sensirion.com/fileadmin/user_upload/customers/sensirion/Dokumente/Humidity_Sensors/Sensirion_Humidity_Sensors_SHT20_Datasheet_V4.pdf "SHT20")  
 * [SPW2430HR5H-B Datasheets](http://www.mouser.com/ds/2/218/-531228.pdf "SPW2430HR5H-B")  
 * [LPS25HB Datasheets](http://www.st.com/content/ccc/resource/technical/document/datasheet/9a/4c/aa/72/1f/45/4e/24/DM00141379.pdf/files/DM00141379.pdf/jcr:content/translations/en.DM00141379.pdf "LPS25HB")  
 * [Sample Code(ble-shepherd)](https://github.com/sivann-tw/hiver-iot-kit-ble/blob/master/example/weatherStation.js "Weather Station Sample Code")
 * [Plugin (ble-shepherd)](https://github.com/bluetoother/bshep-plugin-sivann-weatherstation/blob/master/index.js "Weather Station Plugin")  
