Mindwave Mobile Parser
======================

Simple parser for Mindwave Mobile EEG headsets.
This is a fork from orgicus master branch.
The new version includes now also blink dtection!

How to install the library
==========================

1. [Download the library](https://github.com/orgicus/Mindwave/archive/master.zip)
2. Unzip **Mindwave-master.zip** and rename the **Mindwave-master** folder to the **Mindwave**
4. Move the freshly rename **Mindwave** folder into the **Documents/Arduino/libraries** and restart Arduino


How to use the library
==========================
If you're using the Serial class and simply want to get the attention value,
it's as simple as this.

The example includes also blink detection. A HC-05 is connected to Serial2 in this case.

``` cpp
#include "Arduino.h"
#include "Mindwave.h"

Mindwave mindwave;

void setup() {
  Serial.begin(115200);
  Serial.println("Start");
  Serial2.begin(MINDWAVE_BAUDRATE);
}

void onMindwaveBlink() {
 if (mindwave.blink() == 1) {
    Serial.println();
    Serial.println("Single Blink!");
    Serial.println();   
  }
  
  if (mindwave.blink() == 2) {
    Serial.println();
    Serial.println("Double Blink!");
    Serial.println();
  }
}

void onMindwaveData() {
  Serial.print("Quality: ");
  Serial.println(mindwave.quality());
  Serial.print("Attention: ");
  Serial.println(mindwave.attention());
  Serial.print("Meditation: ");
  Serial.println(mindwave.meditation());  
  Serial.println();
}

void loop() {
  mindwave.update(Serial2, onMindwaveData, onMindwaveBlink);
}
```

For more examples go to **Arduino > File > Examples > Mindwave**

Notes
=====

Be aware, this is my first Arduino library, so things might not be 100% top-notch.
The code is mostly based on the [official NeuroSky wiki article](http://developer.neurosky.com/docs/doku.php?id=mindwave_mobile_and_arduino) and the [ThinkGear protocol specs](http://developer.neurosky.com/docs/doku.php?id=thinkgear_communications_protocol#bit_raw_wave_value)

However, it was developed for the **Focus** project.
This is is covered on the following websites:
 * [Ditte Blohm](http://ditteblohm.com/FOCUS)
 * [Hirsch & Mann](http://www.hirschandmann.com/walking-in-comfort-at-milan-furniture-fair/)
 * [Hackaday.io](https://hackaday.io/project/5969-focus)

 ![Walk With Me](https://cdn.hackaday.io/images/2043671432588591267.jpg)
 ![Walk With Me](https://cdn.hackaday.io/images/8390241432588613274.jpg)
 ![Arduino Shield for DMX and (Mindwave Mobile) Bluetooth](https://cdn.hackaday.io/images/1718121432604763894.jpg)
 
 
