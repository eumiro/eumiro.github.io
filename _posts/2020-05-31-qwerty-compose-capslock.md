---
layout: post
title: "QWERTY with Compose key and without Caps Lock"
tags: keyboard layout international qwerty compose ctrl escape caps lock
author: Miroslav Šedivý
date: 2020-05-31T12:00:00Z
abstract: Use a single keyboard layout for development and for most European languages.
---

**tl;dr then watch this article as a
[lightning talk from PyCon.DE 2019](https://www.youtube.com/watch?v=-4QjII981sM)**

## What keyboard layout are you using?

Are you using _Dvorak_, _Colemak_, _Bépo_, _Neo(2)_ or anything similar?
This article is very probably not for you. You have already invested much more time and
energy to optimize your keyboard input than I did.

However if you just use a standard keyboard layout, such as _QWERTZ_ in Germany or
_AZERTY_ in France, maybe you will find some inspiration in the following lines.

## What are you using your keyboard for?

Shell and programming? In most cases you only need the characters between `\x20` and
`\x7e`:

```
    20      30 0    40 @    50 P    60 `    70 p
    21 !    31 1    41 A    51 Q    61 a    71 q
    22 "    32 2    42 B    52 R    62 b    72 r
    23 #    33 3    43 C    53 S    63 c    73 s
    24 $    34 4    44 D    54 T    64 d    74 t
    25 %    35 5    45 E    55 U    65 e    75 u
    26 &    36 6    46 F    56 V    66 f    76 v
    27 '    37 7    47 G    57 W    67 g    77 w
    28 (    38 8    48 H    58 X    68 h    78 x
    29 )    39 9    49 I    59 Y    69 i    79 y
    2a *    3a :    4a J    5a Z    6a j    7a z
    2b +    3b ;    4b K    5b [    6b k    7b {
    2c ,    3c <    4c L    5c \    6c l    7c |
    2d -    3d =    4d M    5d ]    6d m    7d }
    2e .    3e >    4e N    5e ^    6e n    7e ~
    2f /    3f ?    4f O    5f _    6f o
```

Texts in a human language? You need many more characters. Not only there are very few
minor languages that can be entirely covered by the ASCII encoding listed above,
but for a typographically correct text you usually need further characters, such as
different types of quotes, dashes, and spaces.

## But I have my QWERTZ/AZERTY/…

Yes. Can you comfortably type all the characters from that ASCII list above? And can you
type them with one hand? Keyboard have `Shift` keys on both sides, but not `AltGr`,
which is used by some keyboard layouts to access further characters.

And what if you need to type something in a different language, which is maybe even
a loanword in your own language, such as _résumé_ or _naïve_? Or a name of some foreign
person or place?  Let's say you type in German (QWERTZ) and in French (AZERTY). Do you
switch between the two layouts? Remember where's `A` and `M`? And all those punctuation
marks that are moving around?

This is how a few European keyboard layouts look like when you overlap them:

![]({{ site.url }}/assets/keyboard_chaos.png)

No, thank you.

## Hello QWERTY

I'm using the standard US QWERTY keyboard layout:

![QWERTY]({{ site.url }}/assets/qwerty.png)

because it is widely available. With it the shell, text editor and program languages are
covered.

I write in a few languages every day. Switching between QWERTY/QWERTZ/AZERTY is not an
option. I want one slash on my keyboard, not three.

## Compose key

There was a special key in the 1980s called the **compose key**:

![compose keys]({{ site.url }}/assets/old_compose.jpg)

Press the compose key, press two other keys in sequence, get a character. Works
everywhere on your system: in terminal, browser, text editor, graphic editor, over ssh,
everwhere.

```
⎄ ' a → á      ⎄ ' A → Á
⎄ , c → ç      ⎄ , C → Ç
⎄ " o → ö      ⎄ " O → Ö
⎄ s s → ß      ⎄ S S → ẞ
⎄ c s → š      ⎄ c S → Š
```

No need to press three keys at the same time, no piano player skills required.

My last name _Šedivý_ can be written as `⎄ c S e d i v ⎄ ' y`. With two fingers at most,
where Shift is on both sides of the keyboard, so you can type it while holding a cup of
tea in the other hand.

Now you can have the compose key on your computer. Is there a key you don't use? Menu,
right window, printscreen?

```bash
setxkbmap -option compose:menu
```

Look into `/usr/share/X11/xkb/rules/base` file to see what alternatives to `menu` you've
got.

And then read through `/usr/share/X11/locale/en_US.UTF-8/Compose` to see all
combinations you can use compose key for. Even English speakers “with no need for
characters beyond ASCII” may find following useful:

```
⎄ < " → “      ⎄ < ' → ‘        ⎄ . . → …      ⎄ - - - → —
⎄ > " → ”      ⎄ > ' → ’        ⎄ s o → §      ⎄ - - . → –
⎄ o r → ®      ⎄ o c → ©        ⎄ t m → ™
⎄ < - → ←      ⎄ - > → →        ⎄ m u → µ
⎄ + - → ±      ⎄ % 0 → ‰        ⎄ 1 2 → ½
```

If that's not enough, you can create your own `~/.XCompose` file in similar format to
add new combinations.

## Get rid of the Caps Lock

DO YOU NEED CAPS LOCK? If no, replace it with something useful. How about getting `Ctrl`
closer to your left little finger?

It was there already in the 1970s on ADM-3A terminal on which Bill Joy developed the
`vi` editor (yes, that's where `HJKL` for cursor movements come from).

![adm 3a]({{ site.url }}/assets/adm_3a_terminal.png)

All you need is:

```bash
setxkbmap -option caps:ctrl_modifier
```

combined with the compose key setting:

```bash
setxkbmap -option compose:menu,caps:ctrl_modifier
```

## Where's my Esc?

If you are using the Vim editor frequently, you may wonder why the Escape is so far
away. On the ADM-3A terminal it was so close. But Tab is useful, so let's put Escape on…
_Caps Lock_!

What's the differece between `Ctrl` and `Esc`? You use `Ctrl` in combination with other
keys, while you press `Esc` individually. So if you press `Caps Lock` and then press
some other key, let's consider it to be a `Ctrl`. If you press `CapsLock` and release it
immediately, then let's consider it to be an `Esc`.

Install [xcape](https://github.com/alols/xcape) and start it:

```bash
xcape -e Caps_Lock=Escape
```

## Voilà

Put these two commands into your start scripts:

```bash
setxkbmap -option compose:menu,caps:ctrl_modifier
xcape -e Caps_Lock=Escape
```

and enjoy!

![qwerty]({{ site.url }}/assets/qwerty_power.png)
