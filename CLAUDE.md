# CLAUDE.md

Notes for Claude sessions working on the LED Wiring Planner.

## About the owner
The owner is not a programmer and doesn't know networking or GitHub well. Explain changes in plain language and in detail, and say what to click or check.

## Publishing (standing instruction from the owner)
The owner has said: **auto push for this app.** After every change, once it is tested and committed, push it to the
working branch **and to `main`** (`git push origin <branch>:main`) without asking. `main` is the live GitHub Pages site
(https://videostuff.github.io/LED_Wiring/), so each change goes live a minute or two later. Tell the owner it is live.

## The project
- **`index.html` is the whole app**: HTML, CSS and JavaScript in one file, no build step. Keep it that way.
- Its look (colors, fonts, panels, buttons) is copied from PixelPlanner (`VideoStuff/PixelPlanner`). Keep them matching.
- The script is in numbered sections: 1 library data (`PANEL_PRESETS`, `PROCESSOR_PRESETS`), 2 state, 3 calculation engine (`calc`, `buildChains`), 4 formatting, 5 SVG diagram (`wallSvg`), 6 tables, 7 screen update, 8 events.
- Saved state: `localStorage` keys `ledwiring-state-v1` and `ledwiring-library-v1`; files use `format: 'led-wiring-planner', version: 1`. Keep older files loading after any change to the data shape.
- External resources: Google Fonts only.

## Every change
1. Raise `APP_VERSION` by 0.01.
2. Update `README.md` when something the user can see changes.
3. Test in the pre-installed Playwright/Chromium: no console errors, check the numbers, and check the print view.
4. Commit as `vX.YY: Short plain description`.
5. Push to the working branch and to `main` (see Publishing).
6. Send the owner the HTML to try (copy to the scratchpad as `led-wiring-vX.YY.html`, SendUserFile with `display: "attach"`).
