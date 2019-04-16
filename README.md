IPA keyboard layout for XKB
===========================

All credit for the idea and most of the work getting IPA symbols in some usable form goes to [Abu Jar M Akkas &lt;ajmakkas@ajmakkas.com&gt;](http://www.ajmakkas.com/pages/c_xkbipa.html), inspired by [Mark Huckvale's overlay](http://www.phon.ucl.ac.uk/resource/phonetics/).

Disclaimer: There's no guarantee that any of the files in this repository may be functional. I've made these availble to the public, for free, for your sole amusement. Do whatever you want with them as long as you include a reference to the original author(s).

About
-----

This is a custom keyboard layout for US keyboards which provides access to a number of IPA symbols via "dead keys" (using combinations of Right Alt / AltGr and Shift, plus ordinary keys). It has been tested and seems to work using XKB, and should be fairly easily usable with the majority of Linux distributions.

Some useful links:
- http://linux.lsdev.sil.org/wiki/index.php/Building_an_XKB_Keyboard
- https://wiki.archlinux.org/index.php/X_KeyBoard_extension
- https://www.mkammerer.de/blog/custom-keyboard-layouts-in-cinnamon/
- https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450
- https://www.linux.com/news/creating-custom-keyboard-layouts-x11-using-xkb

Installation
------------

Clone the repository:
```
git clone https://github.com/frekky/xkb-ipa
cd xkb-ipa
```

Add the keyboard layout to your system (must be done as root):
```
sudo -i

cat us.ipa >> /usr/share/X11/xkb/symbols/us
```

Add the following into the appropriate section of `/usr/share/X11/xkb/rules/evdev.xml`:
```
...
  <layoutList>
    <layout>
      <configItem>
        <name>us</name>      
        <shortDescription>en</shortDescription>
        <description>English (US)</description>
        <languageList>
          <iso639Id>eng</iso639Id>
        </languageList>
      </configItem>
      <variantList>
...

<!-- add this bit here -->
        <variant>
          <configItem>
            <name>uclphon</name>
            <description>English (US/intl, with AltGr dead keys for IPA overlay)</description>
          </configItem>
        </variant>
<!-- ----------------- -->

...
      </variantList>
    </layout>
```

Add the following bits into the appropriate sections of `/usr/share/X11/xkb/rules/evdev.lst`:
```
! variant
  intl            us: English (US, intl., with dead keys)
...
  uclphon         us: English (US/intl, with AltGr dead keys for IPA overlay)
...
```

Test that setting the layout works with `setxkbmap us uclphon` (and back to regular US with `setxkbmap us basic`).

Finally you should be able to open Gnome/Cinnamon keyboard settings, and add the layout through the GUI. This will give you access to useful functionality such as using keybindings to switch layouts, and a panel applet which tells you which layout you are on.

Note that the `g` key actually produces a `ɡ` character (which is the IPA symbol for a velar plosive, not a regular ASCII `g`). Be aware this may cause problems if you are typing commands or filenames while using the IPA keyboard.


