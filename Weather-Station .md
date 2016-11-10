# BLE Weather Station Module 
---  

## Guide Content  

1. [Introduction](#Introduction)  
2. [Hardware Overview](#Hardware Overview)  
3. [Usage](#Usage)  
4. [Service & Characteristic UUID](#Service & Characteristic UUID)  
5. [Reference](#Reference)  


<a name="Introduction"></a>
## 1. Introduction  

sivann 的 BLE Weather Station 模組有光度、壓力、溫度、濕度、聲音以及空氣的塵埃 (選擇性，需自己購買 PM 2.5/PM10 加裝) 的感測器。模組上的光度感測器 (Si1132) 可量測紫外線 (UV) 、環境光 (Ambient light)，壓力感測器 (LPS25HB) 可量測大氣壓力，溫溼度感測器 (SHT20) 量測溫溼度而麥克風 (SPW2430HR5H) 量測聲音的響度，其相關的詳細資料在 Reference。  

#### Features  
 * 量測環境光度 (Ambient light)  
 * 量測大氣壓力  
 * 量測溫度、溼度  
 * 量測聲音的變化  
 * 量測空氣塵埃(選擇性)  

#### Spec  
 * 環境光度 (Ambient light ) ：0 – 128k lux  
 * 大氣壓力：260 – 1260 hPa (海拔約1875 – 10100 m)  
 * 溫度範圍：-40 – 120 °C  
 * 溼度：0 – 100 %RH  
 * 分貝計範圍：50–77 dB  


<a name="Hardware Overview"></a>
## 2. Hardware Overview  

此無線感測模組為三種電路模組堆疊而成，包括上層感測模組、中層 BLE 無線模組，以及底層電源模組，如下圖所示。  

![WeatherStation](http://i.imgur.com/edpElLAl.png "WeatherStation")  

### Pinouts  
![WeatherStation Top Module](http://i.imgur.com/5QK3wNmm.png "WeatherStation Top Module")  

* Power Pins:  
  * 5V – 5V的電源腳位。供電給 LM358 及 PM2.5/PM10 (選擇性)  
  * Vcc (3.3V) – 3.3V 的電源腳位。供電給 SPW2430HR5H  
  * Vdd (3.3V) – 3.3V 的電源腳位。供電給 LPS25HB、Si1132 以及 SHT20  
  * GND – 5V、Vcc 及 Vdd 共同的地   
* I2C Pins  
  * SDA – I2C 的資料腳位  
  * SCL – I2C 的時脈腳位  
* P_INT  
LPS25HB 的中斷，發生中斷的情況設定可參閱 Reference 的 LPS25HB  
* UV_INT  
Si1132 的中斷，發生中斷的情況設定可參閱 Reference 的 Si1132  
* MIC  
麥克風 (SPW2430HR5H) 的電壓輸出  
* PM2.5 (選擇性)  
  * Vo1  
  * Vo2  


<a name="Usage"></a>
## 3. Usage  

1. 連接 Micro USB以5V電源供應  


<a name="Service & Characteristic UUID"></a>
## 4. Service & Characteristic UUID

|        Service Name & ID             |  Characteristic Description  |  Characteristic ID  |  Value                   |  Description               |  
|--------------------------------------|------------------------------|---------------------|--------------------------|----------------------------|  
|  **Weather Service (0xBB80)**        |  Barometer Data (R)          |  0xCC11             |  00:00:00:00 (hPa)       |  LSB:00:00:MSB             |  
|                                      |  Temperature Data (R)        |  0xCC07             |  00:00 (°C)              |  LSB:MSB                   |  
|                                      |  Humidity Data (R)           |  0xCC08             |  00:00 (%RH)             |  LSB:MSB                   |  
|                                      |  Ambient Light Data (R)      |  0xCC05             |  00:00:00:00 (lux)       |  LSB:00:00:MSB             |  
|                                      |  Mic Data (R)                |  0xCC1A             |  00 (dB)                 |                            |  
|                                      |  Weather Conf. (R/W)         |  0xBB81             |  0x01 (ON), 0x00 (OFF)   |  Measurement               |  
|                                      |  Weather Peri. (R/W)         |  0xBB82             |  0x0A (10) ~ 0xFF (255)  |  Period = [Input * 10] ms  |  
|  **DIN Service (0xBB00)**            |  DIN Data (R)                |  0xCC00             |  0x01 (H), 0x00 (L)      |  DIN Status                |  
|  **AIN Service (0xBB10)**            |  AIN Data (R)                |  0xCC02             |  00:00 (mV)              |  LSB:MSB                   |  
|                                      |  AIN Conf. (R/W)             |  0xBB11             |  0x01 (ON), 0x00 (OFF)   |  Measurement               |  
|                                      |  AIN Peri. (R/W)             |  0xBB12             |  0x0A (10) ~ 0xFF (255)  |  Period = [Input * 10] ms  |  


<a name="Reference"></a>
## 5. Reference   

[LM358 Datasheets](http://www.ti.com/lit/ds/symlink/lm358.pdf "LM358")  
[Si1132 Datasheets](https://www.silabs.com/Support%20Documents/TechnicalDocs/Si1132.pdf "Si1132")  
[SHT20 Datasheets](https://www.sensirion.com/fileadmin/user_upload/customers/sensirion/Dokumente/Humidity_Sensors/Sensirion_Humidity_Sensors_SHT20_Datasheet_V4.pdf "SHT20")  
[SPW2430HR5H-B Datasheets](http://www.mouser.com/ds/2/218/-531228.pdf "SPW2430HR5H-B")  
[LPS25HB Datasheets](http://www.st.com/content/ccc/resource/technical/document/datasheet/9a/4c/aa/72/1f/45/4e/24/DM00141379.pdf/files/DM00141379.pdf/jcr:content/translations/en.DM00141379.pdf "LPS25HB")  
