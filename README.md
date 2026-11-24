# LED Wiring Planner

Plan the data and power wiring for an LED wall: how many processors and XD boxes you need, how the cabinets are daisy-chained, how many circuits and distro drops to order, and a printable wiring sheet for site. It matches the look of [PixelPlanner](https://github.com/VideoStuff/PixelPlanner).

**Disclaimer:** This tool was created by AI. Panel and processor numbers come from manufacturer spec sheets. Check them against your equipment before you rely on them for a show.

It is a single web page (`index.html`). Nothing to install: open it in a current Chrome, Edge, Firefox or Safari. Your work is saved in your browser and can be saved to and opened from a `.json` file.

## What it does

### LED panel
- Built in: **ROE Diamond DM2.6** (500 × 500 mm, 192 × 192 px, 5.76 kg, 180 W max / 90 W typical) and **ROE Graphite GP2.6** (500 × 1000 mm, 192 × 384 px, 9 kg, 320 W max / 160 W typical), from ROE Visual's spec sheets.
- **Custom panel…** lets you type a cabinet's size, pixels, watts, weight and the voltages it works on. **Add panel to library** keeps it for next time. **Library…** lists every panel and lets you edit or delete your own.

### Wall size
- Set it by **cabinets** (columns × rows), or by **target size** in feet or meters (the closest whole number of cabinets is used).
- Shows the total resolution, total pixels, size in meters and feet, cabinet count and weight.

### Processing (Brompton Tessera SX40 + Tessera XD)
- The SX40 sends four 10G fiber trunks, each to a Tessera XD, which splits it into ten 1G Cat6 ports: up to 40 ports and 9 million pixels per SX40.
- Choose bit depth (8, 10 or 12-bit) and frame rate. **Primary only** or **Full redundancy** (a backup SX40 on each XD's second 10G input).
- Shows each processor's load, for example *1× SX40 — 46% Pixel Load | 8/40 Ports Used*.
- **Custom processor…** for anything else: pixel limit, pixels per 1G port, and either XD boxes or direct 1G ports.

### Data wiring
- Patterns, seen from the rear: **Horizontal snake**, **Vertical snake**, **Top-down**, **Bottom-up**, starting at the rear left or rear right.
- Runs keep to whole rows or columns. Turn on **Fill each port** to pack as many cabinets as fit on each port instead.
- **Data redundancy** adds a backup return line from the last cabinet of each run to its own port (drawn dashed).
- Each run is labeled `D1`, `D2`… with its port load.

### Power
- **120 V**, **208 V 1-phase** or **208 V 3-phase**, breaker size (default 20 A), safety factor (default 80%) and power factor (default 1.0).
- Circuits are sized on **max** watts so a full-white frame can't trip a breaker. Each circuit is labeled `P1`, `P2`… with its amps, and is given a leg (L1, L2, L3 or a pair for 208 V).
- Shows total watts and amps at max and typical load, the load on each leg, and distro drops (default 6 circuits each, for Socapex).

### Diagram
- **Data only**, **Power only** or **Combined**, with **Labels / port load** on or off, in **Rear view** (as the crew sees it) or **Front view**.
- Dots mark where data enters, arrows show its direction, and squares mark where power enters. Hover over a cabinet to see its run and circuit.
- Cabinet numbers are column, row, counted from the front-left.

### Output
- Tiles across the top: processors, XD boxes, 1G home runs, circuits, max amps and resolution.
- Tabs: **Gear list**, **Signal chain** (processor → XD → ports), **Port schedule** and **Circuit schedule**.
- **Print / Export PDF** opens a clean light page: the data diagram and port schedule, the power diagram and circuit schedule, then the gear list and signal chain. Choose **Save as PDF** in the print window to make a PDF.

## The math

**Pixels per 1G port** = 525,000 (Brompton's figure at 8-bit, 60 Hz) × (60 ÷ frame rate) × (24 ÷ bits per pixel). 10-bit is 30 bits per pixel, so 420,000 px; 12-bit is 36, so 350,000 px.
**Cabinets per port** = pixels per port ÷ pixels per cabinet, rounded down (DM2.6: 14 at 8-bit, 11 at 10-bit).

**Processors** = enough that none goes over 9,000,000 px or 40 ports (runs are assigned in order). **XD boxes** = ports used ÷ 10, rounded up, per processor. Data redundancy doubles the ports used. Full redundancy doubles the processors and fiber trunks.

**Usable watts per circuit** = breaker amps × safety factor × volts × power factor (20 A × 80% × 120 V = 1,920 W; at 208 V = 3,328 W).
**Cabinets per circuit** = usable watts ÷ max watts per cabinet, rounded down.
**Amps**: single-phase = watts ÷ (volts × PF). 3-phase (balanced, per leg) = watts ÷ (208 × 1.732 × PF).

## Changing the built-in panels or processor

Open `index.html` in a text editor and find `PANEL_PRESETS` and `PROCESSOR_PRESETS` near the top of the script. Each panel or processor is one line of plain values (sizes in mm, watts, kg). Change a number, save, and reload the page.

## Hosting

To put it online with GitHub Pages: in the repository go to **Settings → Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
