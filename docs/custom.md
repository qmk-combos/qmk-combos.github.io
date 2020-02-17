---
layout: default
title: Custom Engine Config
nav_order: 5
---

# Custom Engines

If you're setting up a board for the first time (and not using the default config) here's the dirty details  
for you. On the other hand if you're just setting things up with the default engine config, skip along to

[Managing Dicts](/docs/manage){: .btn }
 
Sick you're still around, time to get hacking away :) 

So pop open ```keyboards/gboards/g/config_default.h``` that's what we're going to use as a reference here.  
The first thing you'll notice is two defines ```C_SIZE``` and ```COMBO_MAX```.

### C_Size

This is the width of your chords in native AVR types. As of right now the engine supports up to  
64 states. If you're only using a board that uses 10 keys, you can probably squeeze it into a uint16. 

Helpfully, if you have a STN() call of higher then C_SIZE, the compiler will get angry :)

### COMBO_MAX

This is the Maximum number of keys that will be passed to ```KEYS()```, for longer key combos this must  
be overridden to a value that can contain it. Note, this will be the default for _ALL_ combos, so if you  
have one extra extra long combo it might be worth it to turn it into a ```SUBS()``` argument instead

### STN

This is just a wrapper for setting the bit in your chord that gets toggled. Start your symbols at 0 and  
count up. You _must_ end before you overflow C_SIZE!

### COMMAND_MODE

This is the chord for toggling Command Mode, when this is stroked the keyboard starts buffering inputs  
when it's stroked again the combo is sent. It's useful for sending complex combos that would otherwise  
conflict with each other on smaller keyboards

### ENGINE_CONFIG

This section is used by the engine to hook the QMK Keycodes and set the relevant Chord bits, it falls  
through to regular QMK processing if these aren't hooked. You'll need the ending \ is needed!

## Overrideable Functions

Similar to stock QMK there are a handful of functions you can overide to change how the engine functions!  
Just define these in your keymap.c or in another file in your build.  
You should have a good understanding of [this page from the QMK docs!](https://beta.docs.qmk.fm/for-a-deeper-understanding/understanding_qmk#process-record)

### process_engine_post

```C_SIZE process_engine_post(C_SIZE cur_chord, uint16_t keycode, keyrecord_t *record)```

This is run after a key has been matched for the engine. You can use this to set additional bits in a  
chord or modify other keyboard things (Like LEDs!). If you just want to continue processing  
return ```cur_chord```

### process_engine_pre

```C_SIZE process_engine_pre(C_SIZE cur_chord, uint16_t keycode, keyrecord_t *record)```

This is run before _any_ processing has happened. If you return false from here, normal QMK processing  
will happen instead of any engine things. Useful for keeping the engine from running when not on  
a specfic layer or for other uses.

### process_chord_getnext

```C_SIZE process_chord_getnext(C_SIZE cur_chord)```

This is run in the event that a match could not be found. Normally the engine will try smaller and smaller  
bits of the chord until a match is found, but you can return the chord it should try next. Be careful though  
it's easy to end up in infinate loops! Return 0 to continue with normal engine processing.

Hopefully that answers you hackery questions! Good luck on whacking this into your board and extending it!
