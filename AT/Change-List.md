Ai-Thinker GPRS AT module change list
=====

------------------------------------------------
## V1.4:

#### Add feature:

* AT+CCLK:
command `AT+CCLK="AUTO"` can enable auto adjust rtc time on gprs attached, and it will be remembered, cacel auto update time by command`AT+CCLK="YY/MM/DD,hh:mm:ss+zz"`.

* AT+LOCATION
get location(latitude and longitude) through gps or gprs(LBS)

* AT+SPEEDTEST
just for test!!!

#### Remove feature:
None

#### Update feature:

* AT+CCLK:
fixed ack length as as 20. now: "YY/MM/DD,hh:mm:ss+zz"

#### Bug fix:

-------------------------------------------

## v1.0:

#### Add feature:

* AT+AGPS
command `AT+AGP=1` to enable agps

* AT+GIZ****
`AT+GIZSTART` to connect gizwits
`AT+GIZSEND`  to send data to gizwits
`AT+GIZSTOP`  to disconnect from gizwits
`AT+GIZTRACKER` to upload location info to gizwits app
`AT+GIZQRCODE`  save gizwits device QR code string

* AT+GPAUPGRADE
step into upgrade gps firmware mode



