# thoth-big-face

A small change on top of Hermes Gadget `v0.6.0` for the Waveshare ESP32-S3-Touch-AMOLED-2.06:

- **Hero fill** (`DisplayInfo::hero_fill`, on only for the AMOLED 2.06 in `board.cpp`): a colour face is drawn at one size on every hero screen, the largest multiple of 8 that leaves room for a two-line caption. On the 2.06's 410x486 UI area that is 376 px (stock: 192). It shrinks only for answer buttons.
- **Bare idle screen:** with hero fill, the idle screen shows the face alone, with no greeting, cue line or bottom hint bar. A running timer, the interpreter, a profile to pick, notices, low battery and flashed hints still show. Every other screen keeps its text and bar.
- **Plugin:** `plugin/hub.py` accepts colour faces up to 512 px (stock: 256), so Hermes sends the 376 px face.

## Build and install
Run the CI workflow on this branch (Actions → CI → Run workflow) and download the `firmware-esp32s3-touch-amoled-206` artifact. Then patch the installed plugin's `hub.py` the same way and run:

    hermes gadget update "<device name>" <the build's app image>

## Reapply on a new release
    git fetch upstream --tags
    git rebase --onto vX.Y.Z v0.6.0 thoth-big-face

Re-run CI, install the new build, and re-apply the `hub.py` change after any plugin update.

## Back to stock
Install the release's own `hermes-gadget-esp32s3-touch-amoled-206-<version>-app.bin` with `hermes gadget update`, then restore the stock `hub.py`.
