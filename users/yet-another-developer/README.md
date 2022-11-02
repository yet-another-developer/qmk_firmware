# User Space for yet-another-developer

## Reset keyboard
LOWER + KC_LBRC (hold space + [)

## Flashing

Flash
```
cd ~/qmk_firmware
make ergodash/rev1:yet-another-developer:flash
```

Generate build without flashing
```
cd ~/qmk_firmware
make ergodash/rev1:yet-another-developer
```


## Create new layer

Steps
 1. Add keymap matrix in (a). Copy structure of `[_LOWER] = LAYOUT_ergodash_pretty_wrapper(`
 2. In (b) `userspace_layers`, add new layer in enum.
 3. In (c), #define your new layer's L1 L2 L3 R1 R2 R3

Files
 a. qmk_firmware/keyboards/ergodash/rev1/keymaps/yet-another-developer/keymap.c
 b. qmk_firmware/users/yet-another-developer/yet-another-developer.h
 c. qmk_firmware/users/yet-another-developer/wrappers.h 


## Related folders

 - Compiling: users/yet-another-developer/yet-another-developer.c                              [OK]
 - Compiling: users/yet-another-developer/process_records.c                                    [OK]
 - Compiling: users/yet-another-developer/leader.c                                             [OK]
 - Compiling: keyboards/ergodash/ergodash.c                                                    [OK]
 - Compiling: keyboards/ergodash/rev1/rev1.c                                                   [OK]
 - Compiling: keyboards/ergodash/rev1/keymaps/yet-another-developer/keymap.c                   [OK]

## Reference / Inspiration
 - /u/kuchosauronad0
 - /u/drashna
 - /u/not-quite-neo

 ## Layer Activations
 - LOWER: hold left space
 - RAISE: hold right enter
 - ADJUST: hold LOWER + RAISE aka hold left space + hold right enter
 - HYPER: hold key before A (esc), hold key after O (')

## Switching and Toggling Layers
[ref](../../docs/feature_advanced_keycodes.md)
[keycodes](../../docs/keycodes.md)

When using momentary layer switching with MO(), LM(), TT(), or LT(), make sure to leave the key on the above layers transparent or it may not work as intended.

- DF(layer) - switches the default layer. The default layer is the always-active base layer that other layers stack on top of.
- MO(layer) - momentarily activates layer. As soon as you let go of the key, the layer is deactivated.
- LM(layer, mod) - Momentarily activates layer (like MO), but with modifier(s) mod active. Only supports layers 0-15 and the left modifiers: MOD_LCTL, MOD_LSFT, MOD_LALT, MOD_LGUI (note the use of MOD_ constants instead of KC_). These modifiers can be combined using bitwise OR, e.g. LM(_RAISE, MOD_LCTL | MOD_LALT).
- LT(layer, kc) - momentarily activates layer when held, and sends kc when tapped. Only supports layers 0-15.
- OSL(layer) - momentarily activates layer until the next key is pressed. See One Shot Keys for details and additional functionality.
- TG(layer) - toggles layer, activating it if it's inactive and vice versa
- TO(layer) - activates layer and de-activates all other layers (except your default layer). This function is special, because instead of just adding/removing one layer to your active layer stack, it will completely replace your current active layers, uniquely allowing you to replace higher layers with a lower one. This is activated on keydown (as soon as the key is pressed).
- TT(layer) - Layer Tap-Toggle. If you hold the key down, layer is activated, and then is de-activated when you let go (like MO). If you repeatedly tap it, the layer will be toggled on or off (like TG). It needs 5 taps by default, but you can change this by defining TAPPING_TOGGLE -- for example, #define TAPPING_TOGGLE 2 to toggle on just two taps.