#FAQs, additional comments

# Introduction #

This page shows the most asked problems and their solutions.


## Q1: Real values ##

I can not get it to work with REAL. Do you have any examples to communicate with real-variables with Wago 750-841? For example with PLC data as follows?

```
VAR
 TESTVAR1 AT %MD0 : REAL := 100;
 TEST1 AT %MD2 : REAL := 101;
 TEST2 AT %MD4 : REAL := 102;
 TEST3 AT %MD6 : REAL := 103;
END_VAR
```
(Codesys 2.3 code excerpt)

## A1: Real values ##

If you would like to operate with the variables

```
VAR
 TESTVAR1 AT %MD0 : REAL := 100;
 TEST1 AT %MD2 : REAL := 101;
 TEST2 AT %MD4 : REAL := 102;
 TEST3 AT %MD6 : REAL := 103;
END_VAR
```

OK, but I am not sure if you know that your addressing over-jumps
the real values at MD1, MD3 and MD5 memory area of PLC!!! When
you use e.g.

```
// Data to be written
$data = array(1000, 2000, 1.250, 1.250);
$dataTypes = array("REAL", "REAL", "REAL", "REAL");
// e.g. FC23
$recData = $modbus->readWriteRegisters(0, 12288, 6, 12288, $data, $dataTypes);
```

the data will be stored word-by-word into the defined PLC
memory (DWORD == 2xWORDS == 4xBYTES), i.e. from MD0 to MD3. The MD0 and MD2
data in debug mode will not be visible when not used!!!

To change the addressing, use either

```
VAR
 TESTVAR1 AT %MD0 : REAL := 100;
 TEST1 AT %MD1 : REAL := 101;
 TEST2 AT %MD2 : REAL := 102;
 TEST3 AT %MD3 : REAL := 103; 
END_VAR
```

or

```
VAR
 TESTVAR1 AT %MW0 : REAL := 100;
 TEST1 AT %MW2 : REAL := 101;
 TEST2 AT %MW4 : REAL := 102;
 TEST3 AT %MW6 : REAL := 103; 
END_VAR
```

or, if you adhere on this addressing, you should send the modbus request as follows

```
// Data to be written
$data = array(1000, 0, 2000, 0, 1.250, 0, 1.250);
$dataTypes = array("REAL", "REAL", "REAL", "REAL", "REAL", "REAL", "REAL");
// e.g. FC23
$recData = $modbus->readWriteRegisters(0, 12288, 6, 12288, $data, $dataTypes);
```

## Q2: Real-to-float on server side ##

How shall I do if I want to read and show the real values on the PHP side.

## A2: Real values ##

Use the following function

```
// chunk the byte stream (array) to the set of 4 bytes
$values = array_chunk($receivedArrayOfBytes, 4);
// for each call conversion to float
foreach($values as $bytes)
   PhpType::bytes2float($bytes);
```

## Q3: Device is not reachable ##

How to operate the device using the library? The library timeout exceeds!

## A3 ##

To operate the device via Modbus the device IP address and port (502)
must be reachable from server, i.e. it has to be in the same net domain.
To verify it use a ping command from the server.

## Q4: PHPModbus dependencies ##

Library shows the socket functionality is not supported.

## A4 ##

The library uses the PHP socket functionality. For that the server php.ini
should be configured to operate it, i.e. set on the php\_sockets.dll extension.
```
extension=php_sockets.dll
```

## Q5: Modbus RTU and PHP Modbus ##

Does PHP Modbus library support the Modbus RTU?

## A5 ##

The PHP modbus library does not support/implement the Modbus RTU. Modbus RTU protocol is used for RS485 ro RS232 physiscal layer based devices, e.g. Schneider Power Meter, PowerLogic PM750. Any convertor RS485---Ethernet convertor will not help due to the protocol differences.

The recommended way is to read data from the device using a Modbus RTU to Modbus TCP convertor, for example a Ethernet PLC device with RS485 interface that converts (for example PLC Wago 750-881) and read the data via Ethernet Modbus as supproted by the PHP modbus library.

Another way is to use the python library http://code.google.com/p/modbus-tk/, that reads device data directly from a PC serial interface (you need the RS485-RS232 convertor for PM750 like devices).

All is question of technology configuration.

## Q6: Modbus PHP and Beckhoff 9000/9050 ##

Where is the the address MW0 located at Beckhoff 9000/9050? The 0x3000 address reading gets watchdog expiration.


## A6 ##
In accordance to the Beckhoff 9000/9050 manual
([link](http://download.beckhoff.com/download/Document/BusTermi/BCoupler/BK9000en.chm)) the M-memory MB0 is located at 0x4000 not at 0x3000 as in the Wago systems.

For that your code should not point to 0x3000 (MW0 in Wago device)
```
$recData = $modbus->readMultipleRegisters(0, 12288, 5); 
```
but to 0x4000.
```
$recData = $modbus->readMultipleRegisters(0, 0x4000, 5); 
```
For MB10 example addr=0x4000+(10/2)
```
$recData = $modbus->readMultipleRegisters(0, 0x4000+(10/2), 5); 
```