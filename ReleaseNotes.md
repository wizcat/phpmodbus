# Release notes #

## 0.7 -> 0.8.[r106](https://code.google.com/p/phpmodbus/source/detail?r=106) ##
  * Added FC4, FC5 functionality

## 0.6 -> 0.7.[r100](https://code.google.com/p/phpmodbus/source/detail?r=100) ##
  * Fixed [Issue 16](https://code.google.com/p/phpmodbus/issues/detail?id=16)

## 0.5 -> 0.6.[r98](https://code.google.com/p/phpmodbus/source/detail?r=98) ##
  * Added FC2, FC6 functionality
  * Fixed [Issue 13](https://code.google.com/p/phpmodbus/issues/detail?id=13) error code exception
  * Fixed [Issue 14](https://code.google.com/p/phpmodbus/issues/detail?id=14) read coil

## 0.4 -> 0.5.[r70](https://code.google.com/p/phpmodbus/source/detail?r=70) ##
  * Added new TCP functionality
  * Class structure changed, but back compatible

## 0.3 -> 0.4.[r56](https://code.google.com/p/phpmodbus/source/detail?r=56) ##
  * Fixed problem with endiannes declaration ([Issue 10](https://code.google.com/p/phpmodbus/issues/detail?id=10))

## 0.3 -> 0.4.[r53](https://code.google.com/p/phpmodbus/source/detail?r=53) ##
  * Added FC1 and FC15 read/write coils
  * Added FC1, FC15 functionality examples

## 0.2 -> 0.3.[r38](https://code.google.com/p/phpmodbus/source/detail?r=38) ##

  * try-catch functionality
  * PhpType and IecType conversion improvement
  * Improved examples
  * Improved commentaries for documentation

## 0.1 -> 0.2.[r20](https://code.google.com/p/phpmodbus/source/detail?r=20) ##

  * Added new class for conversion from received bytes to PHP data types (PhpType class)
  * Added new data conversion using PhpType example
  * Added new alias methods fc3, fc16 and fc23 (ModbusMasterUdp class)
  * Fixed problems with the endianess when data written (IecType class)
  * Improved commentaries for documentation