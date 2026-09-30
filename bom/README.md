# WavetablePi DigiKey BOM (audio-grade parts)

Bill of materials for the WavetablePi rev0.3 PCB. Parts in or near the audio path were chosen for audio quality. DigiKey part numbers, prices and stock were checked on digikey.com on 2026-09-29 and 2026-09-30.

| File | Contents |
|---|---|
| [WavetablePi_BOM.csv](WavetablePi_BOM.csv) | Full BOM: reference, name, DigiKey and manufacturer part numbers, quantities and prices for 1 and 10 units, footprint, PCB side, silkscreen label, notes |
| [WavetablePi_DigiKey_1unit.csv](WavetablePi_DigiKey_1unit.csv) | DigiKey order for 1 unit |
| [WavetablePi_DigiKey_10units.csv](WavetablePi_DigiKey_10units.csv) | DigiKey order for 10 units |

## Ordering

Upload an order file to the [DigiKey BOM Manager](https://www.digikey.com/BOM), map `DigiKey Part Number`, `Quantity` and `Customer Reference`, then add the list to your cart. DigiKey prints the customer reference (for example `WavetablePi R3 R4`) on each bag, so the parts arrive labelled with their board positions.

The Raspberry Pi Zero 2 W (RPi1) is in the order files, but DigiKey was out of stock on 2026-09-30. If it still is, remove that line and buy the Pi from any approved reseller. It must be the Zero 2 W (the original Zero is too slow) and without a pre-soldered header, because the Pi is mounted flush. DigiKey lists it as SC1176; older SC0510 links lead to the same page.

The order files only contain parts DigiKey sells. You also need:

- **DAC1**: GY-PCM5102 (PCM5102A) I2S DAC module, about 32 x 17 mm, from AliExpress, Amazon or eBay. Check that its form factor and pinout match the PCB, and set the solder bridges as described in the [mt32-pi wiki](https://github.com/dwhinham/mt32-pi/wiki/GY-PCM5102-DAC-module). Use the pin headers supplied with the module.
- **LCD1** (optional): 0.91" SSD1306 I2C 128x32 OLED module with a 4-pin GND/VCC/SCL/SDA header.
- The PCB (see the gerber link in the [main README](../README.md#i-want-to-build-one-myself)).
- A microSD card for mt32-pi (8-32 GB, FAT32).

## BOM for 1 and 10 units

| Reference | Name | DigiKey Part Number | Qty 1 unit | Qty 10 units | Price 1 unit | Price 10 units |
|---|---|---|---:|---:|---:|---:|
| C1, C2 | 10uF 25V X5R ceramic, radial 5mm kinked leads (audio output coupling) | `445-181284-1-ND` | 2 | 20 | $1.00 | $6.00 |
| C3, C4 | 100nF 63V 5% WIMA MKS2 metallized PET film, 5mm pitch (PWM low-pass filter) | `1928-MKS2C031001A00JSSD-ND` | 2 | 20 | $1.36 | $8.46 |
| R1 | 10K 1% 50ppm Vishay Dale CMF55 metal film (MIDI IN level divider) | `CMF10.0KHFCT-ND` | 1 | 10 | $0.61 | $3.94 |
| R2 | 22.1K 1% 50ppm Vishay Dale CMF55 metal film (MIDI IN level divider) | `CMF22.1KHFCT-ND` | 1 | 10 | $0.78 | $5.07 |
| R3, R4 | 1K 1% 50ppm Vishay Dale CMF55 metal film (PWM low-pass filter) | `CMF1.00KHFCT-ND` | 2 | 20 | $1.24 | $7.96 |
| Audio_Select1 | Pin header 2x3 2.54mm vertical, gold flash, breakaway (audio source select) | `35-PRPC003DAAN-RC-ND` | 1 | 10 | $0.12 | $0.99 |
| Audio_Select1 jumpers | Jumper socket 2.54mm, black, open top, gold, 6.00mm | `952-2881-ND` | 2 | 20 | $0.32 | $2.68 |
| RPi1 | Raspberry Pi Zero 2 W (without header) | `2648-SC1176-ND` | 1 | 10 | $15.00 | $150.00 |
| RPi1 header | Pin header 2x20 2.54mm vertical, breakaway (mounts Pi Zero flush to the board) | `35-PRPC020DAAN-RC-ND` | 1 | 10 | $0.95 | $8.06 |
| Wavetable1 | Socket 2x13 2.54mm vertical, gold, 8.50mm (wavetable connector) | `732-61302621821-ND` | 1 | 10 | $1.00 | $9.32 |
| DAC1 | PCM5102A I2S DAC module, GY-PCM5102 (approx. 32 x 17 mm) | not at DigiKey | 1 | 10 | - | - |
| LCD1 | 0.91in OLED SSD1306 I2C 128x32 module, 4-pin GND/VCC/SCL/SDA (optional) | not at DigiKey | 1 | 10 | - | - |
| | **Total (DigiKey order)** | | | | **$22.38** | **$202.48** |
| | Total without the Raspberry Pi | | | | $7.38 | $52.48 |

Prices are DigiKey list prices in USD at the quantity ordered, as checked, and will change. The totals cover the DigiKey order, so DAC1, LCD1, the PCB and the microSD card come on top. DigiKey has no drop-in equivalent for DAC1 or LCD1: its Adafruit PCM5102 and 0.91" OLED boards use different footprints.

## Why these parts

In the audio path:

- **C1, C2 (10 µF output coupling)** are in series with the left and right audio going to the sound card. The usual audio-grade choices, film or a bipolar audio electrolytic such as Nichicon Muse ES, do not fit: the two capacitors sit side by side only 2.67 mm apart, on the side facing the sound card. WIMA's 5 mm-pitch MKS2 film capacitors are already 5 mm thick at 1 µF and stop at 4.7 µF. The 16 V and 25 V 10 µF Muse ES parts (5 mm diameter) are obsolete at DigiKey, and the 50 V one is 8 x 13 mm. The BOM uses a TDK FG28 10 µF 25 V ceramic (4.0 x 2.5 x 5.5 mm), which fits. Assuming a wavetable input impedance of 10 kΩ or more, the -3 dB point is about 1.6 Hz. At 50 Hz only about 3 % of the signal voltage appears across the capacitor, and less at higher frequencies, so the ceramic's voltage coefficient adds very little distortion. A film or bipolar-electrolytic coupling capacitor would need a larger footprint at C1/C2 in a future PCB revision.
- **C3, C4 and R3, R4 (PWM low-pass filter, about 1.6 kHz)**: WIMA MKS2 polyester film capacitors instead of ceramics, and Vishay Dale CMF55 1 % metal film resistors. The ±5 % capacitors set how closely the two channels' filters match, so 0.1 % resistors (`CMF1.0KHBCT-ND`, listed as an alternate) would cost more for little gain. 100 nF C0G ceramics were considered, but at 3.2-3.5 mm thick they are too wide for the gap between the board edge and the Pi.
- **Wavetable1**: Würth WR-PHD 61302621821 socket with gold contacts, 8.5 mm tall. Its 3.1 mm tails stay clear of the OLED, which sits directly above them on the other side of the board. Würth rates it for 25 mating cycles, plenty for a board that is plugged in a few times. If you will move it between sound cards often, the Samtec SSW-113-01-G-D with 20 µin gold is the premium alternative.
- **Audio_Select1 and jumpers**: Sullins PRPC gold-flash header and Harwin M7582-05 gold jumpers, so the audio passes through gold-on-gold contacts. Harwin's gold M20-9980345 header also fits the jumpers and is listed as an alternate; the Sullins one is cheaper. The jumpers are open-top with no handle and 6.00 mm tall, which keeps them short on the side facing the sound card.

Outside the audio path:

- **R1, R2**: Vishay Dale CMF55 1 % metal film. They divide the 5 V MIDI signal from the sound card down to about 3.44 V for the Pi's UART.
- **RPi1 header**: Sullins PRPC020DAAN-RC. It is soldered at both ends with no mating contact, so plating does not matter here. It is a breakaway header, so it snaps into the 2x3 sections the main README recommends. For several boards, the 2x40 version (PRPC040DAAN-RC) is cheaper: break each strip in half for two boards.

## Connector alternates

The connectors were Samtec parts in the first version of this BOM. The parts above are cheaper, well stocked and from established makers; switching saved $5.36 per board, or $49.61 for 10 boards. The trade-off is thinner gold than Samtec's 10-20 µin: the Sullins parts are gold flash, and Würth does not state a thickness but rates its socket for 25 mating cycles. That is fine for contacts that are only mated a few times.

| Reference | In the BOM | Alternates |
|---|---|---|
| Wavetable1 | Würth 61302621821 (`732-61302621821-ND`), gold, $0.93 at 10 | Sullins PPPC132LFBN-RC (`S7116-ND`), gold flash, $1.34 at 10, larger stock; Samtec SSW-113-01-G-D (`612-SSW-113-01-G-D-ND`), 20 µin gold, $3.37 at 10 |
| Audio_Select1 | Sullins PRPC003DAAN-RC (`35-PRPC003DAAN-RC-ND`), gold flash, $0.10 at 10 | Harwin M20-9980345 (`952-2120-ND`), gold, $0.25 at 10; Würth 61300621121 (`732-5295-ND`), gold, $0.46 at 10; Samtec TSW-103-07-G-D (`612-TSW-103-07-G-D-ND`), 10 µin gold, $0.47 at 10 |
| Audio_Select1 jumpers | Harwin M7582-05, black (`952-2881-ND`), $0.13 at 10 | Harwin M7583-05, blue (`952-2882-ND`); Harwin M7581-05, red (`952-2169-ND`); same price |
| RPi1 header | Sullins PRPC020DAAN-RC (`35-PRPC020DAAN-RC-ND`), $0.81 at 10 | Sullins PRPC040DAAN-RC (`S2011EC-40-ND`), 2x40 strip that covers two boards, $1.17 per strip; Harwin M20-9982046 (`952-3299-ND`), tin, $1.14 at 10; Harwin M20-9982045 (`952-3298-ND`), gold, $1.36 at 10; Samtec TSW-120-07-L-D (`612-TSW-120-07-L-D-ND`), $2.60 at 10 |

## Notes

- **R2** is 22.1 kΩ, not the schematic's 22 kΩ, because DigiKey only sells the 22.0 kΩ CMF55 in 1000-piece reels. The Pi's RX pin sees 3.44 V either way.
- **C4** has no value in the schematic ("C"). The main README specifies 100 nF, the same as C3.
- **Btn1-Btn4** are in the schematic but not on the rev0.3 PCB, so they are not in the BOM.
- **PCB side**: "Front" (F.Cu) faces the sound card and holds the Pi. "Back" (B.Cu) holds the DAC, OLED, R3 and R4. The silkscreen shows `10uF` for C1/C2, `10K` for R1 and `22K` for R2.
- **C3, C4**: the 2.5 mm-thick film capacitor is a snug fit between the board edge and the Pi, so seat it toward the board edge.
- **Jumpers**: set them per the silkscreen: 1-2 for the DAC, 2-3 for Pi PWM audio.
