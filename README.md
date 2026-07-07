# Glance

A little monitor app for the Turing 3.5" USB screen. You build your own layouts by dragging widgets around a canvas, then push them to the screen and leave it running next to your keyboard. The name is the whole point: it's a small display you glance at to see how your PC is doing, instead of alt-tabbing to some overlay.

It's a community replacement for the software that ships with the screen. I wrote it because the stock app is closed-source and I wanted something I could actually change and add to.

![The Glance designer: drag widgets onto the canvas, then push it to the screen](docs/hero.png)

## Heads up, this is an alpha

It works, but it's rough around the edges and you will hit bugs. The usual suspects and what to do about them:

- The screen sometimes won't connect on the first try, or it drops out mid-session. Close Glance, unplug the screen, plug it back in, and start it again. That clears up almost everything.
- The Turing panel resets its own COM port when it initializes. If "AUTO" doesn't find it, pick the port by hand. Unplug and replug the screen and watch which COM number appears.
- If the picture looks scrambled after you change orientation, hit Stop and Start again.

Short version: when something acts up, restart the app and reseat the USB cable. I'm still fixing these as I find them, so expect the occasional weirdness.

## What it does

You design screens on a canvas. Drag a widget from the palette on the left, move and resize it, and set its options in the Properties panel. There are fifteen widgets right now: clock, date, text, a stat line, arc and ring gauges, bar meters, a history graph, network up/down with a live graph, battery, weather, and three for whatever music is playing (album art, track text, and a progress bar).

Twelve layouts come built in to start from, including two landscape ones and a "Now Playing" music screen. Duplicate any of them and rework it however you like. New screens save automatically to `%APPDATA%\Glance`, and you can export or import them from the File menu.

![A few of the built-in screens](docs/gallery.png)

A few things worth calling out:

- **Now playing.** It reads whatever's playing on Windows, so Spotify, Apple Music, Cider, a browser, all of it. You get the album art, title, artist, and a progress bar that actually ticks along. There's a "Music only" setting if you'd rather it ignore YouTube and other video.
- **Weather** with no API key and no account. It works out roughly where you are from your IP and pulls current conditions from Open-Meteo.
- **Backgrounds** are per screen: a solid colour, a two-colour gradient, the HUD look with scanlines, or a blurred version of the current album art.
- **Orientation.** Each screen can be portrait or landscape, and there's a global override in the Device panel with upside-down modes for when the panel's mounted the other way. The preview in the editor rotates to match so you can see what you'll get.

![Landscape layouts](docs/landscape.png)

Everything updates live on the panel while you edit, so you can nudge a widget and watch it move on the screen.

## It's built on turing-smart-screen-python

Glance doesn't talk to the hardware itself. The low-level USB protocol comes from [turing-smart-screen-python](https://github.com/mathoudebine/turing-smart-screen-python) by Matthieu Houdebine, which is the reference project for these panels and did the hard work of reverse-engineering the different hardware revisions. That library (its `library/` folder) is bundled here under `vendor/`. Glance is the part on top of it: the widget and rendering system, the designer, and the packaging.

Since that library is GPLv3, Glance is too. See [LICENSE](LICENSE).

It targets the 3.5" Turing screen, hardware revision A, which is the one I have. The other revisions might work if you change the Revision setting in the Device panel, but I haven't tested them.

## Install

### Just run it (Windows)

Download `Glance.exe` from the repo's Releases page and double-click it. It's the whole app in one file, no Python needed. The first time you run it, Windows SmartScreen may warn you about an unknown publisher, since it's an unsigned exe I built myself. Click "More info" and then "Run anyway".

### From source

You'll need Python 3.11 or newer and the screen itself.

```
git clone <your-repo-url> glance
cd glance
python -m venv .venv
.venv\Scripts\activate            # PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
python run_designer.py
```

The driver library is already in `vendor/`, so there's nothing else to download.

To build your own `Glance.exe`:

```
.\build.ps1
```

The first build takes a few minutes. The exe ends up in `dist\` and is around 65 MB, most of that being Qt.

## Using it

Plug the screen in. Over in the Device panel, set the COM port (AUTO usually finds it) and press Start on device. Pick a layout from the Screens list, or hit New and drag some widgets onto the canvas. To have it come up automatically when you log in, tick "Launch at Windows startup".

There's also a headless `main.py` if you just want a fixed dashboard running in the background without the editor. See `config.yaml` for its settings.

## Requirements

- Windows. The now-playing feature uses Windows' media APIs. The rest is cross-platform in theory, but I've only run it on Windows.
- A Turing 3.5" screen (revision A).
- Python 3.11+ if you're running from source.

## Credits

- [turing-smart-screen-python](https://github.com/mathoudebine/turing-smart-screen-python) for the hardware driver.
- [Open-Meteo](https://open-meteo.com/) for the weather, and ipapi.co / ip-api.com for rough location.
- Built with [PySide6](https://doc.qt.io/qtforpython/) and [Pillow](https://python-pillow.org/).

## License

GPLv3, since it builds on GPLv3 code. See [LICENSE](LICENSE).
