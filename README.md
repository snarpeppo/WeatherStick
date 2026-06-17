# Weather Display for M5Stack Atom 1.0

A small **M5Stack** project that displays weather conditions through animations on the built-in LED matrix.

## Features

- Automatic Wi-Fi connection.
- Fallback attempt to a secondary network if the first connection fails.
- Periodic HTTP requests to a remote endpoint that returns a weather code.
- Dedicated animations for different weather conditions:
  - Sunny
  - Cloudy
  - Light rain
  - Heavy rain
- Automatic device reboot if an error occurs while fetching weather data.

## How it works

The device connects to a Wi-Fi network configured in the script and periodically queries a remote endpoint that returns a weather code as plain text.

Based on the returned code:

- `0` → displays the sunny animation
- `1`, `2`, `3` → displays the cloudy animation
- `61`, `63`, `65` → displays the light rain animation
- `80`, `81`, `83` → displays the heavy rain animation

The animations are rendered as RGB frame sequences on the device’s LED matrix.

## Technologies used

- MicroPython
- M5Stack / UIFlow
- Wi-Fi networking
- HTTP requests to a remote endpoint

## Configuration

Before running the project, replace the placeholder Wi-Fi credentials in the script:

```python
wifiCfg.doConnect('XXXXXXXX', 'YYYYYYYY')
wifiCfg.doConnect('JJJJJJJJ', 'KKKKKKKKK')
```

Also make sure the configured weather endpoint is reachable:

```python
req = urequests.get('http://mediapedia.altervista.org/api/m5/weather/')
```

## Notes

The original code contains a logical condition that should be fixed, because in Python expressions like:

```python
elif code == '1' or '2' or '3':
```

always evaluate as true.

The correct form is:

```python
elif code in ['1', '2', '3']:
```

The same issue applies to the other weather code groups as well.

## Possible improvements

- Move credentials and configuration into a separate file.
- Improve network error handling without immediately rebooting the device.
- Support additional weather codes.
- Refactor animation definitions to reduce code repetition.
- Add a serial debug mode.

## License

For personal or educational use, unless otherwise specified.
