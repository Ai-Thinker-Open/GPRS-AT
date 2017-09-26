
Ai-Thinker A9 GSM/GPRS/GPS module AT command set
===

## Gizwits

#### 1. AT+GIZSTART

Connect to Gizwits 
! Before `AT+GIZSTART`, Please ensure your module have the right IMEI, query IMEI by command `AT+EGMR=2,7`,  or set IMEI by command `AT+EGMR=1,7,"your device's IMEI"`(IMEI was set when It produced by Ai-Thinker)

* **(1) AT+GIZSTART= [ Product Key ],[ Product Secret ]**

Sign up gizwits and sign in
! If parameter `Product key` and  `Product Secret` exist, it will sign up gizwits, or (` AT+GIZSTART`) will not sign up, just sign in

|parameter      | type   | brief |
|:--            |  --    |  --   |
| Product Key   | String |  Product key|
| Product Secret| String |  Product secret|
> e.g. 
> AT+GIZSTART="ef285272349f400394e6cc9c37123456","1e9694aabd123456a4f56848fffb83d1"
>> +GIZWITS:sign up end
>> +GIZWITS:sign in end
>> +GIZWITS:conn end
>> 
>> OK
>> 

* **(2) AT+GIZSTART=?**

nuery Command format
> e.g.
> AT+GIZSTART=?
>> +GIZSTART:"product key","product secret"
>> 
>> OK
>> 

* **(3) AT+GIZSTART?**

Query Gizwits connection status
|result         | status |
|--             |  --    |
| 0 |  Not connect |
| 1 |  Registering |
| 2 |  Provision   |
| 3 |  Connecting MQTT server|
| 4 |  Subscribing topic1 |
| 5 |  Subscribing topic2 |
| 6 |  Connected          |
|others|   Error          |
> e.g. 
> AT+GIZSTART?
>> +GIZSTART:6
>> 
>> OK
>> 


#### 2. AT+GIZSTOP
Disconnect from gizwits
No parameter
> e.g.
> AT+GIZSTOP
>> OK
>> 

#### 3. AT+GIZSEND
publish data to Gizwits

* **(1) AT+GIZSEND=< action >,[ n ],[ data ]**

|parameter      | brief  |
|--             |  --    |
| action        | gizwits action( e.g. device upload data:4)|
| n             |  data num, >= 0, or not set: then module Response `>`, then type data for send, tap `CTRL+Z`(`0x1A`)  to complete send.|
| data          | string data to send, if not set but `n` was set, then module Response `>`, then type `n` data for send, end up with `Enter(\r\n)`|
> e.g.
> AT+GIZSEND=4,5,"12345"
>> OK
>  
> AT+GIZSEND=4,5
>> \> 
>
> 12345
>> OK
> 
> AT+GIZSEND=4
> 
>> \> 
> 
> 123456\x01\x00\x02\x05\x1A
>> OK
>>   


* **(2) AT+GIZSEND=?**

> e.g. 
> +GIZSEND:< action >,[len],[data]
> 
>> OK
>> 


* **(1) AT+GIZSEND?**

> e.g. 
> +GIZSEND:status:0
> 
>> OK
>> 

#### 3. AT+GIZQRCODE
just for save gizwits device qrcode string in flash

* **(1)AT+GIZQRCODE=<"QRCODE STRING">**
save QR code string

* **(2)AT+GIZQRCODE?**
get saved QR code string

## Tracker（Gizwits）

#### 1.AT+GIZTRACKER
GPS tracker: gizwits as server
! Firs ensure you have correct IMEI(`AT+EGMR=2,7`) 

* **(1) AT+GIZTRACKER=< on/off >,[server],[upload interval],[use LBS],[pk],[ps]**

|   parameter      |  brief    |
|   --             | --        |
|   on/off         |  value:0/1 as off/on,if set to 1, it will auto startup use settings before  |
|   server         |  select server, `0`:Ai-Tinker official, `1`:custom(parameter `[pk]` and `[ps]` are required at the fisrt time use this command, module will save this two parameters onece connect success)          |
|   upload interval|  upload position interval (s). Value `defaul to 0(do not upload) `        |
|   use LBS       |   whether use LBS to get location when gps can not get location.`0`:only use gps(so it will not upload location info when gps can not get location),`1`:get location info from LBS. Value `default to 0`.|
|   pk            |  product key |
|   ps            |  product secret|

> e.g. use Ai-Thinker official gizwits server
> AT+GIZTRACKER=1,0,10
>> +GIZTRACKER:Start
>> OK
>>  +GIZWITS:sign in end
>> +GIZWITS:conn end
>> 
>> OK
> 
> AT+GIZTRACKER=0
>> 
>> OK

* **(2) AT+GIZTRACKER=?**
> e.g.
> AT+GIZTRACKER=?
>> 
>> +GIZTRACKER:<0/1>,[0/1],[n],["pk"],["ps"]
>> 
>> OK
> >

* **(3) AT+GIZTRACKER?**

response:+GIZTRACKER:< isOn >,<  upload interval >
|   parameter      |  brief    |
|   --             | --        |
|   isOn         |  value:0/1 as off/on,if set to 1, it will auto startup use settings before  |
|   upload interval|  upload position interval (s)         |
> e.g.
> AT+GIZTRACKER?
>> 
>> +GIZTRACKER:1,10
>> 
>>OK
>>

## AT+CCLK="auto"

Auto set time when gprs attached

## AT+LOCATION

* **(1)AT+LOCATION=<LBS or GPS>**

Get positioin through LBS server(Ai-Thinker)
|parameter| value|
|---|---|
|LBS or GPS |value `1`:get location info through LBS, `2`:get location by GPS(GPS should be open first by `AT+GPS=1`) |
return: 
> `<latitude>,<longitude>`
> OK

 
> e.g
> AT+LOCATION=1
> 
>> 22.608901,113.841279
>> 
>> OK


## AT+GPSUPGRADE

Release GPS UART from A9's CPU, then you can connect GPS UART directly to communicate with GPS. `!!`If not release GPS connection, the RX pin of GPS(TX of CPU) MUST connect nothing

* **(1)AT+GPSUPGRADE=<on/off>**

|parameter|value|
|-|-|
|on/off|`1`:release GPS's connection from CPU, `0`:connect GPS to A9's CPU|

## AT+SPEEDTEST

* **(1)AT+SPEEDTEST=< data size >,< times >**


