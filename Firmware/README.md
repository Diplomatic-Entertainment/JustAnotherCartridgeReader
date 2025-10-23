## This Arduino sketch is licensed under the GNU GENERAL PUBLIC LICENSE Version 3 (GPL v3)    

### This means that you are free to:    
- use, modify and distribute this software, even commercially    

### Under the following terms:    
- state changes   
- disclose source   
- same license   

### Limitations:
- Liability   
- Warranty   

More details: https://www.gnu.org/licenses/gpl-3.0.en.html    

## 

Every submodule has it's own setup_XX() function that configures the needed pins and a submenu that lets you choose what you want to do. 
The code directly addresses the pins via the DDR, PIN and PORT registers.   
Please also refer to the [pinout Open Office sheet](https://github.com/sanni/cartreader/blob/master/pinout.ods).    
```
void setup_N64_Controller() {  
  // Output a low signal  
  PORTH &= ~(1 << 4);  
  // Set Controller Data Pin(PH4) to Input  
  DDRH &= ~(1 << 4);  
}  
```

Would be the same as this in a more traditional Arduino sketch:  
```
int dataPin = 7;   

void setup(){    
  // Output a low signal   
  digitalWrite(dataPin, LOW);   
  // Set controller data pin to input  
  pinMode(dataPin, INPUT);  
}  
```
To preserve memory every string is saved into the flash of the Arduino, also called progmem. This is done by using the F() macro.   
```
println_Msg(F("Press Button."));  
```
Also all the menus are stored in progmem and are only recalled to sram when needed.  
```
// N64 controller menu items  
const char N64ContMenuItem1[] PROGMEM = "Test Controller";  
const char N64ContMenuItem2[] PROGMEM = "Read ControllerPak";  
const char N64ContMenuItem3[] PROGMEM = "Write ControllerPak";  
const char* const menuOptionsN64Controller[] PROGMEM = {N64ContMenuItem1, N64ContMenuItem2, N64ContMenuItem3, FSTRING_RESET};
```
In an effort to keep the codebase as portable as possible instead of using the functions supplied by the OLED library directly to print out text, auxiliary functions like `println_Msg` are being used. So if you want to change to another display library you don't need to change all the code but only the helper functions. 
```
void print_Msg(long unsigned int message) {
  if (ENABLE_OLED)
    display.print(message);
  if (ENABLE_SERIAL)
    Serial.print(message);
}
```

For more info please have a look at [this wiki article](https://github.com/sanni/cartreader/wiki/How-to-flash-the-Arduino).   

Needed libraries(already included in the portable Arduino IDE under Releases)   

SD lib: https://github.com/greiman/SdFat    
LCD lib: https://github.com/olikraus/U8g2_Arduino     
Neopixel lib: https://github.com/adafruit/Adafruit_NeoPixel    
Rotary Enc lib: https://github.com/mathertel/RotaryEncoder    
SI5351 lib: https://github.com/etherkit/Si5351Arduino        
RTC lib: https://github.com/adafruit/RTClib (needs BusIO lib: https://github.com/adafruit/Adafruit_BusIO)     
Frequency Counter lib: https://github.com/PaulStoffregen/FreqCount    

### JACR Modifications 
- Renaming directory from cart_reader to firmware forced cart_reader.ino to be renamed firmware.ino
  - Added JACR as hardware refernce where HW5 is also defined
- Modified config.ino
  - JACR is currently based on the HW5 revision
  - Noted to not change HW selection
  - Noted to not enable VSELECT
  - Clock Generator enabled
  - RTC enabled
  - Noted to not enable 3V3FIX (not needed on JACR)
  - Noted to not enable Stability Fix (not need on JACR)
  - Noted to not enable the updated (untested, unlikely to work with intended results) 
  - Enabled SNES Core/CLOCKGEN by default
  - Comment out ifelse for HW Type
- Modified oscr.h
  - Comment out sanity checks to save some bytes
  - Updater baud rate commented out to save bytes
  - CS_8MHZ commented out to save the bytes
  - ENUM for VSELECT & 3V3FIX commented out (unused on JACR)
- Modified oscr.cpp
  - Added JACR suffix to FSTRING_VERSION
  - Changed FSTRING_OSCR from OSCR to JACR
  - Comment out setClockScale VOLTS and CLKSCALE
  
