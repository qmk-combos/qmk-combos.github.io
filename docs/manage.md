---
layout: default
title: Managing Dictionaries
nav_order: 5
---

# Managing dictionaries

Now for the fun part! Managing (and most likely creating) dictionaries. There are two main types of
dictionaries: Combo dictionaries (```combos.def```) and Chording dictionaries (```dicts.def```) 

If you're here off the begining, there's going to be more creating dictionries than just importing
them. Be sure to PR your dictionaries against [qmk-combos/combos](https://github.com/qmk-combos/combos)
any PRs are appriciated!

## combos.def
Let's start with an example
```
#include "combos/germ-vim-helpers.def"// Important for work!
#include "combos/germ-mouse-keys.def"
//#include "mycombos.def"
```

Seems pretty straight forward eh? This is just C code that gets embedded. So you can do // or /* */ style
comments. The dictionaries will be templated in. To add new ones just add a #include statement, to remove
them either delete the line or prefix it with //

## dicts.def

Example: 

```
#include "dicts/aset/en-keymap.def"
#include "dicts/aset/cmd-keymap.def"
#include "dicts/aset/num-keymap.def"
#include "dicts/aset/layer-keymap.def"
#include "user.def"
```

The format is exactly the same as combos.def, but should only be loaded with chorded dictionaries
In this example if we wanted to change the ASETNIOP language we would just change the first include
to something like de-keymap.def _einfach!_

## Prefixes

Some dictionaries support a special variable PREFIX, this can be optionally defined before including a
.def. The prefix will be added to any included definitions. Here's an example for how to use these:

**NOTE**: You must include the trailing '\|' or ',' and remember to #undef it after

combos.def:
```
#define PREFIX KC_Z, 
#include "combos/germ-mouse-keys.def"
#undefPREFIX
```

dicts.def:
```
#define PREFIX GZ |
#include "combos/germ-mouse-keys.def"
#undefPREFIX
```


# Best Practices 

- Keep defs small and constrained to a context (Mouse keys, Text shorthands, Firefox-Shortcuts, etc...)
- Remember .defs can include other .defs, break it up!
- Use PREFIX where it makes sense! If all of your movements are using KC_S, change it to prefix!
- A blank prefix can be done with "#define PREFIX " and omitting the last argument
- Submit them back (we don't bite!)

## Using PREFIX in a .def
Because a user _may_ override this, provide a blank or sensible default. You can do this as such. In addition
the | or , is ommitted from the definition. 
Combos:
```
#ifndef PREFIX
#define PREFIX 
#endif 

COMB(str10, KC_ESC, PREFIX KC_W, KC_E)
...
```
Chords:
```
#ifndef PREFIX
#define PREFIX GS | 
#endif 

SUBS(PREFIX GA,str10, "How to use a prefix!")
...
```
