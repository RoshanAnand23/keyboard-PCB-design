The purpose of this logbook is to write down my thought process, and reasons for my decisions. It is not an actual step by step process to make the keyboard.







///////////////////////////////////////////////////////////////////////////////////





Starting with figuring out how the overall structure of a keyboard PCB layout is structured

(SUMMARY: schematic have whole circuit with footprints, then in PCB design, arrange them)



**Plugins** used with Kicad(to consider):

**HTML BOM**: list of materials



**place footprints:** makes moving components(that has footprints assigned) easier(even spacing)



**round tracks**:smooth already routed tracks(purely aesthetic, idk if will use)



**Simple Libraries:** many components(symbol+footprint) included



\*\*KiCad library for Arduino modules:\*\*makes it easy to include Arduino mc(dont even need to assign footprints)



**JLC:** fabrication toolkit???(haven't added) So that, after finish design, files formatted to directly order PCB









**Understanding Keyboard Matrix and Direct Wiring**

Direct Wiring: grid of switches, each switch has a dedicated controller pin



**Matrix**(with diode):each column and row has a dedicated controller pin

A column connects to one side of the switch pin, while  each row is connected to a diode connected to the other switch pin

Controller sends a pulse into the matrix and listens on the other end of the matrix. Depending on its voltage level, it correspond to a specific switch being detected









//////////////////////////////////////////////////////////////////////////////



**Starting the Design:**(Do more research before starting)



* Getting a library that includes the mechanical switches schematics and footprints

(https://github.com/joe-scotto/scottokeebs/tree/main/Extras/ScottoKicad)

(https://github.com/kiswitch/kiswitch/tree/main)should be included in the above



* In schematic: set up switch+diode, and generate the matrix
* wire up(row and column)
* place controller and connect row/columns to pins on controller
* assign pcb footprints to schematic(hopefully library has footprints)
* In PCB: Update PCB(bring components to PCB designer)
* Set grid according to components spacing, and set origin point

TIP:3D viewer to see where physically placed, can place within the white space accordingly

TIP: Consider which layer to place everything

* Route everything, and run outline
* Run DRC
* Fieldzone
* Extract for fabrication(JLC)

TIPS: surface finish, HASL(basic and affordable), ENIG(expensive).









**FIRMWARE:**

Considering using either using QMK firmware(https://qmk.fm/), or ZMK firmware(https://zmk.dev/docs/features/split-keyboards).



QMK is for wired connection, better if i were to make a single wired keyboard,

ZMK is ideal for wireless split keyboard

Keymap code: https://nickcoutsos.github.io/keymap-editor/









**From my understanding**, QMK would be the easier to set up, it is done in c(i have experience), and the process seems much more straightforward.

However, I have decided to use ZMK, namely for the wireless feature since that would be more practical for daily use.



**What i must consider considering i am using ZMK:**

* Understand GitHub actions(on a basic level)
* Include batteries(and potentially a BMS) into the circuit design: Based on the boards/lipo battery i am planning to use, it should be fine.
* consider a new layout that involves split screen.
* *FOR FUTURE: Dongle option to improve battery capability(sounds link ZMK makes the upgrade process really easy*





















**Components:**

I need to consider components that are compatible with ZMK, and ideally able to handle a battery module(https://zmk.dev/docs/hardware)



**Puchi-BLE V1**(https://keycapsss.com/keyboard-parts/mcu-controller/202/puchi-ble-wireless-microcontroller-pro-micro-replacement)

Has an on/off switch, Li-Po battery charger (4.2V Lithium @ 100mAh)

*Only use LiPo batteries with a protection circuit, because the Puchi-BLE has no low voltes (discharge) protection for batterie*s

*NOTE: It is the orange tape(with some electronics) at the top of the battery*

30 euros^^ would most likely get the component quicker

**NOTE: An Arduino Pro Micro replacement, so can use the same footprint**



**nice!nano**(https://kriscables.com/product/nicenano/?utm\_source=nicekeyboards\&utm\_medium=referral\&utm\_campaign=find-a-store)

Would probably be the easiest to set up, similar to above.

30 euros



Reminder: Before you solder or plug any battery into one of these wireless boards, ALWAYS check that the red wire is going to B+ and the black wire is going to B- / GND



**Keycap:**

Site for keycaps etsy: (https://www.etsy.com/listing/1441551215/xda-blank-keycap-custom-keycap-custom?ls=a\&ga\_order=most\_relevant\&ga\_search\_type=all\&ga\_view\_type=gallery\&ga\_search\_query=low+profile+apple+keycaps\&ref=sc\_gallery-1-7\&sr\_prefetch=1\&pf\_from=market\&pro=1\&sts=1\&plkey=Eu2sJL2uWpj7TboUaT-fakflYq70%3ALT6e985c341e1baf15e20121c1e7fb9c842215bf55\&variation0=6185040888)



(https://www.amazon.co.uk/FOLODA-Keycaps-Personality-Supplement-Computer-Gray/dp/B0CKQPH9QP/ref=sr\_1\_21?crid=1LK2SXJO84A7P\&dib=eyJ2IjoiMSJ9.9TcicRQ-rgKeEsNZG88xXLxir6P\_1TdJPyPi\_bPpOVRlI9VsAPUJmKdEcnApjwK0sD14xHNgxxC1w7OOTFtR-0KD0CZ6Br9V\_P6C4kYQKPHnoDjwTCLJcRE41oqWaBqqAuXJw0kvHorDIuKu3gco69qyufa7iXuEmeriqBgeEXlXVDhp0hKiE6JO0AjRF8FeOxP802vEY7YdbfzsHmPSV5kNHRNltvJghV5p7aRRMa4.g8c0JSJD08KC\_qEKMFl7d42ffLOe74vAW9He-7DhH7I\&dib\_tag=se\&keywords=XDA%2Bprofile%2C%2BDSA%2Bprofile%2C%2Bor%2BMOA%2Bprofile%2Bblank%2Bkeycap\&qid=1787031320\&sprefix=xda%2Bprofile%2Bdsa%2Bprofile%2Bor%2Bmoa%2Bprofile%2Bblank%2Bkeycap%2Caps%2C336\&sr=8-21\&th=1)



XDA profile, DSA profile, or MOA profile



Key Switch:

MX style: Haimu Whisper Silent Tactile Switch

(https://cannonkeys.com/products/haimu-whisper-silent-tactile-switch?srsltid=AfmBOoqKRaLQne966JjXv\_auseRBswyh\_EF\_Zi8NprU\_BSAoJcHOmYEl)



Alternatively: https://prototypist.net/search?q=Haimu+Whisper+Silent+Tactile+Switch

Has many more options, in smaller packs, easy to find Cherry MX Equivalent





















////////////////////////////////////////////////////////////////////////////



**STARTING**

Now starting it on kicad(i will make the layout later)

Basic steps

* Get the library on kicad and start it(schematic)  (DONE)
* work on layout                                    (DONE)
* **Make left side(and duplicate project and rearrage for right side**
* Make 3D Printed case
* fabricate and order components(mc, switches, caps)
* solder
* flash
* hopefully it works











##### GETTING LIBRARY ON KICAD-left



I used DownGit to download the specific folder from (https://github.com/joe-scotto/scottokeebs/tree/main/Extras/ScottoKicad), and then added them to my leftKeyboard and rightKeyboard project folders. These were the libraries where the symbol/footprints were from)



Then I added the libraries to the project specific library

How to get there:(main menu, preferences, manage symbol/footprint libraries, project specific library)



NOTE: Do not need to create/modify the path.

NOTE: Schematic are mainly for the MC, the switches would just use the normal switch schematic, and only the footprint would be what is needed from the library



**(HAVENT DONE THIS STEP FOR THE RIGHT KEYBOARD)^^**





##### SCHEMATIC-left



I started placing the switch, diode and Controller schematics(for left Keyboard)



The pinout for the controller(https://help.keycapsss.com/build-guides/puchi-ble/)



I was slightly confused by the pinout:

I believe Pin1(which is on the top left of the schematic, corresponds to the top right of the pinout microcontroller which shouldn't actually impact the schematic too much, as long as i am careful during the PCB step)

Explanation shown in *Pinout comparison.docx)*



I decided that i will solder the battery directly to the MC post fabrication, but it is worth noting that the pinout shows the Bat+ and Bat- to be to the sides of the usb port(top)



NOTE OF PIN connections in schematic vs corresponding pinout:

Col1-pin5 D1

Col2-pin6 D0

Col3-pin7 D4

Col4-pin8 C6

Col5-pin9 D7

Col6-pin10 E6



Row1-pin11 B4

Row2-pin12 B5

Row3-pin15 B1

Row4-pin16 B3



**After understanding the pins, and know what to keep track of during the PCB stage, the schematic of the left keyboard is done.**



* Potentially add a reset button for the reset pin?





##### FOOTPRINTS-Left

Assigning footprints to the components



With the library that i had already added to project, I should just need to add apply the footprints.

Considering the components i am using, the switches should follow the Cherry MX style, or something equivalent. the diodes should be the od35s diode(footprint included in library)





I had an issue where i couldn't see the libraries' footprint. I later discovered that i need to add the folders with the .pretty into the list, not the entire parent footprint folder



For the diode I assigned the D035 diode(from the scottokeebs library

NOTE: To quickly find components, select library on the left side, before searching



for key switch, 1u, 2u all determines what type of key it is,

**I will be using: 1u is the normal ones,** 

**I will use 1.25u for (CTRL(s1), CAP(s7),SHIFT(s13),NUMLAYER(s19),TAB(s20),del(s21)**

**I will use 1.5u for the space(s22) and enter**



NOTE: 1u up to 1.17u all use the same keyswitch, only differentiating key cap size. Any larger ones would need stabilizers



Controller already had its footprint assigned







NEXT STEP: 

Consider adding the rst button to schematic

Finish PCB for left keyboard

do schematic for right keyboard











