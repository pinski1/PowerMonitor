# Power Monitor
I wanted to monitor the current and voltage of some battery packs as I discharged them. As the battery packs were >36V fully charged there was no available board to do this easily. So here's one that's good for up to 80V.

This project is an entry into the [Hackaday.io](Hackaday.io) [Square Inch Project](https://hackaday.io/contest/160135-the-return-of-the-square-inch-project) Contest.

## Detailed Description

This project makes use of the Analog Devices [LTC4151](http://www.analog.com/en/products/monitor-control-protection/power-monitors/ltc4151.html) to measure the voltage, current and communicate these values over an I<sup>2</sup>C bus. In addition the LTC4151 will also calculate the instantaneous power and read an auxilary ADC input, in my board I've set this to be a temperature sensor.



### I<sup>2</sup>C Address
By default the I<sup>2</sup>C address is set to 0xD4 but if you wish to change it please consult this table:

|JP1|JP2|Address|
|----|----|----|
|X|X|0xCC|
|L|H|0xCE|
|H|NC|0xD0|
|H|H|0xD2|
|NC|NC|0xD4|
|L|NC|0xD6|
|H|L|0xD8|
|NC|H|0xDA|
|NC|L|0xDC|
|L|L|0xDE|

### Registers

|Register Address|Register Name|Read/Write|Description|
|--|--|--|--|
|0x00|SENSE (A)|R/W|ADC Current Sense Voltage Data (8 MSBs)|
|0x01|SENSE (B)|R/W|ADC Current Sense Voltage Data (4 LSBs)|
|0x02|VIN (C)|R/W|ADC VIN Voltage Data (8 MSBs)|
|0x03|VIN (D)|R/W|ADC VIN Voltage Data (4 LSBs)|
|0x04|ADIN (E)|R/W|ADC ADIN Voltage Data (8 MSBs)|
|0x05|ADIN (F)|R/W|ADC ADIN Voltage Data (4 LSBs)|
|0x06|CONTROL(G)|R/W|Controls ADC Operation Mode and Test Mode|
|0x07-0xFF|Reserved|N/A|Remaining addresses reserved|

Note: Registers A-F are only writeable if bit G4 is set.

### Calculating Current

+7V to +80V input range
81.92mV V_sense maximum
0R002 => 40.96A maximum
0R002 3.2W resistor 

### Calculating Temperature
[Thermistor](http://uk.farnell.com/panasonic-electronic-components/ertj1vs104fa/thermistor-ntc-0603-100k/dp/1892612)


## Licence
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/80x15.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
