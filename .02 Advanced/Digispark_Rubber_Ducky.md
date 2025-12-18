# Key Modifiers
``` Arduino
#define MOD_CONTROL_LEFT    (1<<0)
#define MOD_SHIFT_LEFT      (1<<1)
#define MOD_ALT_LEFT        (1<<2)
#define MOD_GUI_LEFT        (1<<3)
#define MOD_CONTROL_RIGHT   (1<<4)
#define MOD_SHIFT_RIGHT     (1<<5)
#define MOD_ALT_RIGHT       (1<<6)
#define MOD_GUI_RIGHT       (1<<7)
```
``` Arduino
git https://github.com/digistump
```

# DigiQuack Pack

``` Git
https://github.com/CedArctic
```

// Converted using digiQuack by CedArctic (https://github.com/CedArctic/digiQuack) 


``` Arduino
#include "DigiKeyboard.h"

void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

  DigiKeyboard.delay(1000);
  DigiKeyboard.sendKeyStroke(0);
  DigiKeyboard.sendKeyStroke(KEY_N, MOD_CONTROL_LEFT);
  DigiKeyboard.delay(600);
  DigiKeyboard.print("https://youtu.be/dQw4w9WgXcQ?t=43s");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);

  for(;;){ /*empty*/ }
}
```


