# STM32MP257F-EV1 (MB1936 Rev E): KiCad 10 project

A KiCad 10 conversion of STMicroelectronics' reference design for the
STM32MP257F-EV1 evaluation board (board MB1936, revision E), made from ST's
Altium Designer design files. Converted and maintained by
[creopus](https://github.com/creopus).

> **Unofficial.** This conversion is not affiliated with, endorsed by or
> supported by STMicroelectronics. The design belongs to STMicroelectronics and
> is used under ST's Open Platform License Agreement; see [License](#license).

## Open the project

Requires KiCad 10.0.8 or newer. Clone the repository and open
`MB1936.kicad_pro`.

## Status

- **Schematic ERC:** 0 errors. The 13 warnings are nets that deliberately carry
  two names, and 415 findings are reviewed exclusions.
- **Board DRC** (zones refilled, schematic parity on): 0 errors, 0 warnings,
  0 unconnected items. The 108 exclusions are ST's layout as fabricated, each
  with a review comment.
- **Schematic and board are in sync:** Update PCB from Schematic reports no
  changes, and all 853 board footprints match the project footprint library.
- **Checked against ST's manufacturing files** for MB1936 Rev E (Gerber, drill,
  pick-and-place): the placement of all 806 fitted parts, the drill holes and
  slots, the tracks, pads and vias on all six copper layers, the solder mask and
  the solder paste are identical. The copper pours agree with ST's within 1% of
  the copper area on each layer.

## Contents

| Path | Contents |
|---|---|
| `MB1936.kicad_pro` | KiCad project |
| `MB1936.kicad_sch` and 18 sheet files | Schematic |
| `MB1936.kicad_pcb` | Six-layer board |
| `MB1936.kicad_dru` | Custom design rules, taken from ST's Altium rules |
| `*.kicad_sym` | Three project symbol libraries |
| `MB1936-import-fps.pretty/` | Project footprint library (89 footprints) |
| `empty.kicad_wks` | Empty drawing sheet, so ST's own frame and title block stand alone |

Design variants: `MP257F_X` (ST's X2 variation) and `MP257F_X_OSC` (40 MHz
oscillator instead of the crystal). `kicad-cli` exports the BOM and position
files per variant with `--variant`.

## Notes

- **Via mask openings.** ST's solder mask opens 1,970 vias on each side at
  hole + 0.1 mm. KiCad 10 sizes a via opening only from the via diameter and the
  board-wide mask expansion, so these openings are filled circles on `F.Mask`
  and `B.Mask`, in the groups `ST via mask openings F (hole + 0.1 mm)` and
  `ST via mask openings B (hole + 0.1 mm)`. The vias themselves are tented. If
  you move or delete one of these vias, move or delete its circles as well.
- **The DRC check "Silkscreen clipped by solder mask" is set to ignore.** ST's
  silkscreen crosses about 350 of its own via openings, more than KiCad can keep
  as reviewed exclusions. Board houses normally clip silkscreen at mask
  openings.
- **Logos.** The CE, WEEE, ESD, RoHS, recycling and ST logos on the silkscreen
  are ST's outlines, as filled polygons.
- **Connectivity.** ST's package does not include the Altium harness
  definitions. The connections between sheets were rebuilt and checked against
  the routed board.
- **`kicad-cli` parity check.** `kicad-cli pcb drc --schematic-parity` reports
  108 `net_conflict` items that the KiCad GUI does not. They come from default
  net names that include a unit letter, and can be ignored.

## License

The design files are STMicroelectronics' *Reference Material*, licensed under
ST's **Open Platform License Agreement** (<https://www.st.com/opla>). This
repository is a modified copy (a conversion to KiCad format) and is distributed
under the same agreement. The agreement allows the Reference Material to be
used, modified, copied and distributed for the purpose of evaluating, testing
and developing application boards based on ST products. By using these files
you accept its terms, which include:

- The material may not be offered for sale, sold or leased.
- ST's name, logo and other trademarks may not be used to endorse or promote
  products derived from it without ST's prior written permission. The board
  artwork carries ST's logo, as in ST's design: remove it from boards you derive
  from this design unless ST permits otherwise.
- The material is provided "as is", without warranty of any kind.

No other licence is granted; see [LICENSE.txt](LICENSE.txt).

Copyright © 2025 STMicroelectronics.
