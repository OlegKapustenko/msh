# Robot board 2_1

## Disclaimer

Flashing custom firmware can brick your device. Proceed at your own risk.

## Quick start

You can find the whole process of build if you want to do it yourself.
If you would like to take a shortcut, here it is.

```bash
# Setup the virtual env first
python3 -m venv .venv
. .venv/bin/activate
pip install -U pip
pip install esptool

# Flashing
esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash 0x0 firmware.factory.bin
```

## Board identification

It took a while to identify the board since I thought it is a Heltec 2.0.
I tried to flash many versions of firmware but none of them was working well.
So, Gemini suggested to choose the criteria I have to check and try to
build my own based on the stable version (2.7.15 for that moment).
Here is the list of checks
- battery, it must show correct value for external and battery power
- radio, no errors, I can message a board on the same channel
- screen, it shows what I need
Once again, I succeeded do not damage my board, but if you manage to fire
your own down, it is only your responsibility, not mine!

## How it was built

The source was taken from the official [Meshtastic repo](https://github.com/meshtastic/firmware)
```bash
/meshtastic/firmware$ git branch
* (HEAD detached at v2.7.15.567b8ea)
  develop
```

Here is the build process.

- Setup the virtual env first

```bash
# Setup the virtual env first
python3 -m venv .venv
. .venv/bin/activate
```

- Prerequisities
```bash
pip install -U pip
pip install platformio mklittlefs esptool
```

- The build
```bash
pio run -e heltec-v2_1
ls -l .pio/build/heltec-v2_1/
```

- Flashing
```bash
esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash 0x0 firmware.factory.bin
```

Good luck!

