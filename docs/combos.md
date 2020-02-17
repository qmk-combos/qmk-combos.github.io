---
layout: default
title: Combo Docs
nav_order: 2
---

# Parts of a Combo

Using this library with combos you have two functions avalible for use ```SUBS``` and ```COMB```. 
They stand for Substitute and Combo respectfully. Lets take a look at a dictionary

germ-vim-helpers.def
<script src="https://gist.github.com/germ/49787a86b5693f79b21ef1e3549595c1.js?file=germ-vim-helpers.def"></script>

## COMB()
The ```COMB()``` Macro is responsible for take in a combo and outputting ***a single keypress!***. The general form is ```COMB(ident, keycodeToEmit, keySequence...)``` So Line 3 in the above dictionary takes WE and outputs Escape. 

***Ident***:A unique identifier, something descriptive works, but asdfffdsadf also works.

***keycodeToEmit:***A keycode from the [QMK Keycode list](https://beta.docs.qmk.fm/features/keycodes_basic). This includes Mouse, Shifted and Quantum keycodes.

***keySequence:*** a series of keycodes to be pressed before triggering this output.

## SUBS()
Subs is a very powerful macro and is used for all other sequences. For multicharacter, shifted or well _anything else_ you're going to use SUBS. At it's core it relys on QMKs SEND_STRING()
The general form is similar to COMBs, ```SUBS(ident, sendStringArg, keySequence...)```. So Line 10 outputs
the start of the Interjection copypasta.

***Ident***:A unique identifier, something descriptive works, but asdfffdsadf also works.

***sendStringArg:*** The macro or string to be send by SEND_STRING()

***keySequence:*** a series of keycodes to be pressed before triggering this output.

## Advanced SEND_STRINGing
The strings passed to SUBS() can be much more then dumb output! For sending control sequences, modifiers 
and other abritrary keycodes take a look at the [QMK SEND_STRING docs](https://github.com/qmk/qmk_firmware/blob/master/docs/feature_macros.md#tap-down-and-up). Just be aware that this library handles the hooking and storage, just pass the string to SUBS()!

Take a few minutes to play around and make a few of your own and add them to your ```combos.def```! Next up, managing dictionaries.

[Managing Dicts](/docs/manage){: .btn .btn-primary }
