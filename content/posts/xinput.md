---
title: "Xinput"
date: 2021-01-25T21:58:56+08:00
lastmod: 2021-01-25
author: "xiaonan"
math:
 enable: true

tags: [xinput]
categories: [linux]
---

To disable a laptop's internal keyboard

### xinput list[^Is there a way to disable a laptop's internal keyboard?]
[^Is there a way to disable a laptop's internal keyboard?]: [Is there a way to disable a laptop's internal keyboard?](https://askubuntu.com/questions/160945/is-there-a-way-to-disable-a-laptops-internal-keyboard)

Execute the command `xinput list` to list input devices.

```bash
$ xinput list
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ ETD2303:00 04F3:3083 Mouse                id=11   [slave  pointer  (2)]
⎜   ↳ ETD2303:00 04F3:3083 Touchpad             id=12   [slave  pointer  (2)]
⎜   ↳ ETPS/2 Elantech Touchpad                  id=17   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Power Button                              id=8    [slave  keyboard (3)]
    ↳ Video Bus                                 id=9    [slave  keyboard (3)]
    ↳ XiaoMi USB 2.0 Webcam: XiaoMi U           id=10   [slave  keyboard (3)]
    ↳ Intel HID events                          id=13   [slave  keyboard (3)]
    ↳ Xiaomi WMI keys                           id=14   [slave  keyboard (3)]
    ↳ Xiaomi WMI keys                           id=15   [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=16   [slave  keyboard (3)]
```

### Locate `AT Translated Set 2 keyboard`

take note of its `id` number

### disable the keyboard

xinput float <id#>, where <id#> is the keyboard's id number. For example, if the `id` was `10`, then the command would be `xinput float 16`

### re-enable the keyboard

`xinput reattach <id#> <master#>`

- `master` is that second number we noted down. For example, if the `master` was `3`, you would do `xinput reattach 16 3`

