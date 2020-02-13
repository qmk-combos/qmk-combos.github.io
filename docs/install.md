---
layout: default
title: Installation Guide
nav_order: 1
---

# Install

Lets get this party started, you'll need a [QMK Powered Keyboard](https://qmk.fm/), a working [QMK build environment](https://beta.docs.qmk.fm/newbs/newbs_getting_started). and your own keymap. Once you have those set up, come on back. If you're using a newer [g Heavy Inudstries](https://www.gboards.ca)/ board these may be enabled already!

Still here? Awesome. Let's edit your setup. Pop open your keymaps ```rules.mk``` and add this somewhere. If there isn't a ```rules.mk``` file in your keymap, create it!

```
VPATH  +=  keyboards/gboards/
COMBO_ENABLE=yes
```

This line lets the compiler know where to look for combos. Now make a empty file named ```combos.def``` in your keymap directory. That's it!

### Your first combo
In ```combos.def``` add this statement.
```SUBS(helloWorld,       "QMK is pretty rad eh?",       KC_H, KC_J)```

Save it, compile your keymap and flash it. If you've done it correctly pressing H and J
at the same time will output the text. Congrats!

If you're not enabling the Chording Engine, head on over to

[Creating Combos](/docs/combos.md){: .btn .btn-purple }

### Chording 

If you wish to use the onboard chording engine, a little bit more tweaking needs to be done. Until I remove this todo, take a look at Ginny [in this branch](https://github.com/germ/qmk_firmware/tree/ginny-improv/keyboards/ginny) works.

Here's a short list

-- Setting up rules.mk
-- Creating dicts.def
-- Choosing C_SIZE
-- Creating ENGINE_CONFIG

// TODO: Describe the build process
