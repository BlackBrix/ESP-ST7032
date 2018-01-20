Arduino library for I²C-LCD-Displays with controller ST7032i  

forked from [weizenbock/ESP-ST7032](https://github.com/weizenbock/ESP-ST7032)  
which is forked from [tomozh/arduino_ST7032](https://github.com/tomozh/arduino_ST7032)  
  
  
the (translated) original readme.md is as follows:  

--------------------------------------------------

ST7032 - Arduino LiquidCrystal compatible library
http://ore-kb.net/archives/195

-------------------------------------------------------------
 Overview
-------------------------------------------------------------

I²C LCD display using ST7032i as controller
It is an Arduino library.
It is based on the original Arduino LiquidCrystal library source.
Because it is compatible with the member functions of the original Arduino LiquidCrystal library,
you can use it just by replacing the class.

Operation has been confirmed with:

    SB1602B             Strawberry Linux
    SB0802G             Strawberry Linux
    AQM0802A-RN-GBW     http://akizukidenshi.com

What seems to work:

    SB1602E             Strawberry Linux
    LCD16X2-I2C         aitendo
    SPLC792-I2C-M       aitendo
    16X2-SPLC792-I2C    aitendo


-------------------------------------------------------------
Change log:
-------------------------------------------------------------

2014.10.13 Fixed a problem that the contrast value bit 7 affects the BON bit
2014.08.23 I made it possible to set the I2C address in the constructor
2013.05.21 1st release


-------------------------------------------------------------
 License:
-------------------------------------------------------------

Author:  
tomozh (tomozh@gmail.com)

License form：
MIT


-------------------------------------------------------------
 Instructions:
-------------------------------------------------------------

1) Connect LCD-module and Arduino as follows
``  ------------------------
    Arduino        ST7032
    ------------------------
    3.3V    --+-- VDD  
              +-- -RES  
    A4(SDA) --*-- SDA  
    A5(SCL) --*-- SCL  
    GND     ----- GND  
  
    *... 10Kohm pull-up  
    ------------------------
``

If you want to reliably reset the LCD, connect the RST pin to Arduino's  
Please control with empty terminals. (Low: reset)  
 
2) Copy the ST7032 folder to Arduino's libraries folder  


There are two types of member functions unique to ST7032:  

    constructor
       ST7032 lcd(int i2c_addr);
            i2c_addr: Slave address
            if the constructor argument is omitted: default 0x3E

    Contrast setting
        void setContrast(uint8_t cont)
            cont: Contrast value (0 .. 63)
    
    Icon display (on LCDs without icon display function: this is ineffective)
        void setIcon(uint8_t addr, uint8_t bit)
            addr : Icon address (0 .. 15)
            bit  : Icon display bit (0x00 .. 0x1F)

Easy to use:  
  
    #include <Wire.h>  
    #include <ST7032.h>  
  
    ST7032 lcd;  
  
    lcd.setContrast(30);            // Contrast setting  
    lcd.print("hello, world!");  
  
  
When needed to specify the slave address:  
    
    ST7032 lcd(0x3E);  
  


-------------------------------------------------------------
 file structure:
-------------------------------------------------------------
```
ST7032\  
    keywords.txt  
    ST7032.cpp              ST7032 Library  
    ST7032.h                ST7032 Library  
    examples\  
        Icon                Icon display demo for Strawberry Linux SB1602B  
        Autoscroll          (*)  
        Blink               (*)  
        Cursor              (*)  
        CustomCharacter     (*)  
        Display             (*)  
        HelloWorld          (*)  
        Scroll              (*)  
        SerialDisplay       (*)  
        setCursor           (*)  
        TextDirection       (*)  
  
        (*) examples taken from original Arduino LiquidCrystal liblary modified for ST7032  
```

