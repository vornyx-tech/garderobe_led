# garderobe_led

ESPHome firmware for wardrobe (garderobe) LED lighting on an ESP32-C3 SuperMini.
It drives two white LED strips through MOSFETs and exposes them to Home Assistant
as two dimmable lights:

| Light                 | Section                     | Pin   |
|-----------------------|-----------------------------|-------|
| **Garderobe Clothes** | left – hanging clothes      | GPIO3 |
| **Garderobe Shelves** | right – shelves             | GPIO4 |

Each light supports on/off and brightness, with a smooth fade and restore-after-power-loss.

## Flashing

1. Install ESPHome:
   ```sh
   pip install esphome
   ```
2. Create your secrets file and fill it in:
   ```sh
   cp secrets.example.yaml secrets.yaml
   openssl rand -base64 32   # paste the output as api_encryption_key
   ```
3. Plug the ESP32-C3 SuperMini in via USB and flash:
   ```sh
   esphome run garderobe-led.yaml
   ```
   Choose the USB serial port when asked. If the board isn't detected, hold **BOOT**,
   tap **RESET**, then release **BOOT** and try again.
4. Later updates can be flashed over Wi-Fi with the same command (choose the network option).

Once it's online, Home Assistant will discover it automatically. Add it there and
enter the `api_encryption_key` when prompted.

## Wiring notes

- Use logic-level MOSFETs (fully on at 3.3 V gate voltage).
- Add a ~10k pull-down resistor from each MOSFET gate to GND so the strips stay off while the ESP boots.
