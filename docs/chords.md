---
layout: default
title: Chording Docs
nav_order: 3
---

# What is a Chord? What is a Combo?

There is a fundamental difference between the two! A Combo is a native QMK
feature and only applies to multi-key sequences and SEND_STRING(). However
it can't handle layering, processing strokes in chords and many other things
required on smaller or heavily chorded keyboards! The Chording engine is the
solution to this, but only has limited interoperability with QMK.

If you are only using Combos for _augmenting_ a keymap, don't use the chording engine, use the Combos!

## Function Docs

If you have not read the Combo Docs, give those a quick browse. The format used for these chords is similar.
Back? Awesome.

There are four functions that you can call in a dictionary, they are 

```PRES(chord, keyOut)``` : Send a single QMK keycode  
```KEYS(chord, id, keys)``` : Send a sequence of keypresses  
```SUBS(chord, id, string)``` : Send Strings and sequences  
```SPEC(chord, func, arg)``` : Trigger Special functionality/QMK Interop  

And you can use these to make any chorded dictionary! 

## Usage: 
example.def (excerpts from en-keymap.def)

```
PRES(GA,                                  KC_P)                        // Send P
KEYS(GA|GO,        cmb_9df323cdb026f7ce,  {KC_LSFT, KC_9, COMBO_END})  // Send (
SUBS(GR|GI|GO|GP,  str_E21E9A5405E9A529,  "pool ")                     // "pool "
SPEC(GA|GT|GN|GP,  SPEC_STICKY,           NUM)                         // Activate StickyBit for NUM
```

Notes:

-- Only QMK Basic Keycodes can be sent using this engine. For shifted stuff you _must_ use ```KEYS()```!
-- ID can be set to whatever, however it _must_ be unique. If it's not the compiler will yell at you
-- For KEYS the brackets must be included, or the compiler will yell at you.

## SPEC()

There's a few special things that can be done through this code that changes how the engine operates. Heres 
a table of the currently implemented stuff

KeyCode | Arg | Function
-|-|-
SPEC_STICKY | Chord     | This set's/removes the specified bits from stickybits
SPEC_REPEAT | none      | Toggle the repeat mode until toggled off
SPEC_CLICK  | Keycode   | Send the specified mousekey to the mouse subsytem. Requires mousekeys
SPEC_SWITCH | QMK Layer | Turn on the given layer. The user is left to change back to the chorded layer

## Chords 

A chord is just a bitmask made by or'ing together keys. These keys are defined in your ```ENGINE_CONFIG```  
section. When the listed keys are pressed the action is run. The engine will match the longest chord possible!

The default engine mappings are below, if you're doing a custom engine yours will be different. If you're doing 
this on a normalish keyboard, just make a layout with the following keycode (using the function keys for 
your thumb keys!

QMK Keycode | Chord Equivelent
-|-
KC_Q|GQ
KC_W|GW
KC_E|GE
KC_R|GR
KC_T|GT
KC_Y|GY
KC_U|GU
KC_I|GI
KC_O|GO
KC_P|GP
KC_A|GA
KC_S|GS
KC_D|GD
KC_F|GF
KC_G|GG
KC_H|GH
KC_J|GJ
KC_K|GK
KC_L|GL
KC_SCLN|GCL
KC_Z|GZ
KC_X|GX
KC_C|GC
KC_V|GV	
KC_B|GB	
KC_N|GN	
KC_M|GM	
KC_COMM|GLT
KC_DOT|GGT
KC_SLSH|GQU
KC_F1|GL1
KC_F2|GL2
KC_F3|GL3
KC_F4|GR3
KC_F5|GR2
KC_F6|GR1		


Clear as mud? Good! Go take a look at some of the dictionaries, they'll make more sense now :)


[Custom Engines](/docs/custom){: .btn }
[Managing Dicts](/docs/manage){: .btn .btn-primary }
