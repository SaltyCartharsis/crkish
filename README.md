# Corne keyboard

The Corne keyboard is a split keyboard with 3x6 column staggered keys
and 3 thumb keys, based on [Helix](https://github.com/MakotoKurauchi/helix).
Crkbd stands for Corne Keyboard.

![v4](https://github.com/foostan/crkbd/assets/736191/bc32e4e8-f737-4516-b92b-55a7cb93a336)

## Latest versions
- corne-cherry: for Cherry MX compatible switches

  - v4 Hotswappable ([JP](docs/corne-cherry/v4/buildguide_jp.md)/[EN](docs/corne-cherry/v4/buildguide_en.md))
  - v4 Soldering (will be released)
- corne-chocolate: for Kailh choc v1 and v2 switches
  - v4 Hotswappable ([JP](docs/corne-chocolate/v4/buildguide_jp.md)/[EN](docs/corne-chocolate/v4/buildguide_en.md)):
  - v4 Soldering (will be released)

## Old versions

- corne-classic: for Cherry MX compatible switches 
  - v1 Soldering: ([JP](docs/corne-classic/buildguide_jp.md)/[EN](docs/corne-classic/buildguide_en.md))
- corne-cherry: for Cherry MX compatible switches
  - v2 Hotswappable: ([JP](docs/corne-cherry/v2/buildguide_jp.md)/[EN](docs/corne-cherry/v2/buildguide_en.md))
  - v2 Hotswappable tilting version: ([tilting, JP](docs/corne-cherry/v2/buildguide_tilting_tenting_plate_jp.md)/[tilting, EN](docs/corne-cherry/v2/buildguide_tilting_tenting_plate_en.md)):
  - v3 Hotswappable: ([JP](docs/corne-cherry/v3/buildguide_jp.md)/[EN](docs/corne-cherry/v3/buildguide_en.md))
- corne-chocolate: for Kailh choc v1 switches
  - v2 Hotswappable: ([JP](docs/corne-chocolate/v2/buildguide_jp.md)/[EN](docs/corne-chocolate/v2/buildguide_en.md)):
- corne-light: for easy build with a simple PCB
  - v1 Soldering: ([JP](docs/corne-light/v1/buildguide_jp.md)/[EN](docs/corne-light/v1/buildguide_en.md)):
  - v2 Soldering: ([JP](docs/corne-light/v2/buildguide_low_edition_jp.md)/[EN](docs/corne-light/v2/buildguide_low_edition_en.md)):

## Notice
There are currently reports of a bug in v4.* caused by electromagnetic interference. Depending on the environment, one or both of the left and right keyboards may stop working. It is known that this is often caused by EMI emitted by mobile phones. If you experience this kind of problem, reconnect the USB, move the EMI-generating device (probably a mobile phone) more than 30 cm away from the keyboard, and observe the situation.

For more details, please see this issue. We look forward to receiving any new information.
https://github.com/foostan/crkbd/issues/265

## This fork

This repository is [SaltyCartharsis/crkish](https://github.com/SaltyCartharsis/crkish), a fork of [foostan/crkbd](https://github.com/foostan/crkbd). Work recorded here stays on this fork.

The board under work is the corne-cherry v4 hotswap, silk rev 4.1.0, in `pcbs/corne-cherry/hotswap/`. Chocolate, classic, light, and the soldering variant are unchanged.

### Done

JLCPCB placement for the Kailh hotswap sockets, commit `72aa9fd`:

- `jlcpcb/production_files/CPL-corne-cherry.csv` places all 46 CPG151101S11-16 sockets (LCSC C5156480) on the midpoint of the two socket pads. The previous coordinates were the key center, 3.86 mm away. Rotations are the same. The switch holes were not moved.
- `jlcpcb/production_files/BOM-corne-cherry.csv` lists that same part on three lines: 40× 1u, 2× 1.5u (`SW1`, `rSW1`), and 4 encoder positions (`EXSW1`, `EXSW2`, `rEXSW1`, `rEXSW2`). Encoders are not populated.
- The LCSC land pattern is about 0.26 mm wider than the pads drawn in this footprint. The placement origin is the midpoint of the pads on this board, and the contacts still fall on the 2.55 mm pads.
- The KiCad footprint origin is still the key center, which is the center the plate uses. A new position export from KiCad will put the sockets back on the key centers. The pick-and-place file is the one that has to keep the socket center.
- Gerbers were not regenerated. The commit changes the BOM and the CPL only.

### Planned

- Have a shop in the United States fabricate and assemble this cherry v4.1.0 hotswap, including sourcing the parts. One keyboard is one panel with both halves. The board is 2-layer, 1.6 mm, 1 oz copper, about 277.2 × 107.5 mm, with mousebites and no v-score. Assembly is bottom-side SMT. The USB-C connector has to be TYPE-C-31-M-13C (LCSC C2848620). The TRRS jacks are through-hole. The per-key LEDs are reverse-mount SK6812MINI-E. Vendor choice and a firm quote are still open.
- The phone interference described above is still in the design. On this PCB the USB D+ and D− runs are about 115–119 mm from the USB-C receptacle to the 27 Ω series resistors, a quarter-wave near 635 MHz, inside the n71 phone band (617–698 MHz). The top ground pour covers roughly half of that run. The trace from the RP2040 to the TRRS jack is 89 mm on the left and 96 mm on the right, a quarter-wave near 840 MHz and 780 MHz. On the right half the top ground covers about 10% of that trace. The jack is tip = 5 V, ring = TX, sleeve = GND, so the cable between halves continues the conductor. The USB-C A and B pins of each pair are joined by about 34 mm of trace. These lengths were measured on the v4.1.0 board. The copper was left as routed, because moving those traces on this two-layer stack would shift the resonances into another phone band. Clearing the fault means a new layout with a continuous ground under a short USB pair. That respin has not been started.

## Images

### Cherry
![corne-cherry](https://github.com/foostan/crkbd/assets/736191/f954ba89-a711-4866-a535-bad0bed937d1)
![image](https://github.com/foostan/crkbd/assets/736191/6a6705d2-40fb-4463-8006-6b7ca97dc0ff)
![image](https://github.com/foostan/crkbd/assets/736191/20407f6c-0f2e-41ea-8cd6-17d46d9be0a2)

### Chocolate
![corne-chocolate](https://github.com/foostan/crkbd/assets/736191/fb0e6962-76b3-4bd5-8093-83ccc1a17029)
![image](https://github.com/foostan/crkbd/assets/736191/610f9964-3adf-459b-88ad-9e9f29d5f659)
![image](https://github.com/foostan/crkbd/assets/736191/134db4dd-0c48-4a5f-bf75-97b8e652be22)

### Drawing
![sketche](https://github.com/foostan/crkbd/assets/736191/87ebea53-3c5c-42a1-97b3-f9292e4dacae)
