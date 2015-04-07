# PhpModbus #

This project deals with an implementation of the basic functionality of the Modbus TCP and UDP based protocol using PHP.

Implemented features:
  * Modbus master
    * FC1 - Read coils
    * FC2 - Read input discretes
    * FC3 - Read holding registers
    * FC4 - Read holding input registers
    * FC5 - Write single coil
    * FC6 - Write single register
    * FC15 - Write multiple coils
    * FC16 - Write multiple registers
    * FC23 - Read/Write multiple registers

[![](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=PCZY3Z2623XTU)

Example:
```
require_once dirname(__FILE__) . '/Phpmodbus/ModbusMaster.php'; 

// Modbus master UDP
$modbus = new ModbusMaster("192.168.1.1", "UDP"); 
// Read multiple registers
try {
    $recData = $modbus->readMultipleRegisters(0, 12288, 5); 
}
catch (Exception $e) {
    // Print error information if any
    echo $modbus;
    echo $e;
    exit;
}
// Print data in string format
echo PhpType::bytes2string($recData); 
```

For more see [documentation](http://code.google.com/p/phpmodbus/downloads/list) or [FAQ](http://code.google.com/p/phpmodbus/wiki/FAQ).

Note:
  * The PHP extension php\_sockets.dll should be enabled (server php.ini file)


