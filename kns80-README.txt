The Bendix/King KNS 80 (version 1.2)
------------------------------------

This implementation is build according to the user manual.
The meaning of course deviation is depending on the active mode:
- VOR: deviation represent +/-10° (like a normal NAV radio)
       (if ILS is dedected it represent +/-4°)
- VOR PAR: deviation represent +/-5nm (parallel mode)
- RNV ENR: deviation represent +/-5nm (Areal NAV en-route)
- RNV APR: deviation represent +/-1.25nm (Areal NAV approach)
Every mode normalize the representation to +/-1 in
    '/instrumentation/kns80/nav/heading-needle-deflection-norm'.

If you want bind a CDI, HSI, DG to the system,
you will find all needed values under '/instrumentation/kns80/nav/'.

All buttons are normal push buttons.
The volume knob can be rotated with the mouse wheel and
pushed/pulled with shift+click.
The outer knob can be rotated with the mouse wheel
The inner knob can be rotated with the mouse wheel and
pushed/pulled with shift+click.
The ILS annunciator will lit if the radio receive a ILS frequency.


Include the KNS 80 in your aircraft:
------------------------------------

- copy the 'kns80' directory inside your aircraft tree
    (as example to 'Models/Interior/Panel/Instruments/')

- add the 'kns80.xml' to your panel (like every other model)

- add a 'nav-radio' and a 'dme' in your instrumentation
    (under <sim> … <instrumentation>)
    its a good idea to set the power source of the nav-radio and dme to the source
    of the KNS80
    as example:

        <nav-radio>
            <name>nav</name>
            <number>1</number>
            <power-supply>/systems/electrical/outputs/kns80</power-supply>
            <minimum-supply-volts>24</minimum-supply-volts>
        </nav-radio>

        <dme>
            <name>dme</name>
            <number>1</number>
            <power-supply>/systems/electrical/outputs/kns80</power-supply>
            <minimum-supply-volts>24</minimum-supply-volts>
        </dme>

    If you have a older version of FGFS (prior April 2023), the properties
    <power-supply> and <minimum-supply-volts> will not be supported!
    In this case, make sure that the radios have power if the KNS 80 is turned on.

- open the file 'kns80-config.xml' and configure all aliases to the right nav and dme

- add the file 'kns80-proprules.xml' as property rule under '<sim> … <systems>' in your set-file

- include the file 'kns80-props.xml' under '<instrumentation>' in your set-file like:

        <kns80 include="../relative/path/to/kns80-props.xml">

- copy the file 'kns80.nas' into your Nasal directory and add it in your set-file
    under '<nasal>' in your set-file like:

        <kns80>
            <file>Nasal/kns80.nas</file>
        </kns80>

- open the file 'kns80.nas' and edit the first line so that it can find 'kns80-config.xml'



Handling of KNS 80 by external hardware
---------------------------------------

Some user want bind buttons on the joystick or yoke to interact with devices in the virtual cockpit.
Some build there own hardware with RaspberryPi or Arduino and connect it via network or serial.
This KNS 80 has now a simple interface to interact with external hardware.
The KNS 80 reside in the property tree under '/instrumentation/kns80/'.
Inside there is a directory '/event/' where every button and knob has its own event handler.

Buttons are boolean properties.
If you press a button, set the property to 'true' (1), if you release it, set it to 'false' (0).

Possible buttons are:
    button-vor
    button-rnav
    button-hold
    button-use
    button-dsp
    button-data

Knobs are integer properties.
If you rotate a knob clockwise, increase the value, if you rotate it counter clockwise, decrease the value.

Possible rotating knobs are:
    knob-volume
    knob-outer
    knob-inner

Some knobs can also be pulled or pushed. This properties are boolean and they work like a switch.
If you pull it out, set the property to 'true' (1), if you push it in, set it to 'false' (0).

Possible pull/push knobs are:
    knob-volume-pull
    knob-inner-pull



Happy flying :)
Sascha Reißner
2023
