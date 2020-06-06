---
layout: default
title: Installation Guide
nav_order: 1
---

# Install

Lets get this party started, you'll need a [QMK Powered Keyboard](https://qmk.fm/), a working [QMK build environment](https://beta.docs.qmk.fm/newbs/newbs_getting_started). and your own keymap. Once you have those set up, come on back. If you're using a newer [g Heavy Inudstries](https://www.gboards.ca)/ board these may be enabled already!

## **Combos**


Still here? Awesome. Let's edit your setup. Pop open your keymaps ```rules.mk``` and add this somewhere. If there isn't a ```rules.mk``` file in your keymap, create it!

```
VPATH  +=  keyboards/gboards/
COMBO_ENABLE=yes
```

This line lets the compiler know where to look for combos. Now make a empty file named ```combos.def``` in your keymap directory. 

In ```keymap.c``` add ```#include "g/keymap_combo.h"``` just after ```#include QMK_KEYBOARD_H```. This will include your combos into the compile process.


Lastly add this to your ```config.h``` in your keymap directory. It's optional, but helps with errors from typing too fast! ```#define COMBO_TERM 50```

## Your first combo
In ```combos.def``` add this statement.
```SUBS(helloWorld,       "QMK is pretty rad eh?",       KC_H, KC_J)```

Save it, compile your keymap and flash it. If you've done it correctly pressing H and J
at the same time will output the text. Congrats!

If you're **not enabling the Chording Engine**, head on over to

[Creating Combos](/docs/combos){: .btn .btn-primary}

## Chording 

If you wish to use the onboard chording engine, a little bit more tweaking needs to be done. The easy way is to grab a preconfigured board, but in lieu of that, there's a default config that is tuned for QWERTY, you can use this as a base it's over in ```gboards/g/config_default.h```, copy this to your keymap folder as ```config_engine.h```

You'll need to edit ```rules.mk``` as follows: 

```
VPATH               +=  keyboards/gboards/ 
SRC                 +=  g/engine.c 
```

Make a file called ```dicts.def``` and add this statement:
```SUBS(GD | GF,     undef1, "Oh yeah, it's all coming together.")```

If you've done everything correctly, your firmware should compile and output that string when DF is pressed!
Head on over to the next section for how to import existing dictionaries and whatnot

[Creating Chords](/docs/chords){: .btn .btn-primary}
