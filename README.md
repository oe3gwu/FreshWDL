# FreshWDL

FreshWDL is a lightweight, pure JavaScript alternative to **Weather Display Live (WDL)**, which originally relied on Flash. It runs in any modern web browser and works on nearly any device or platform.

This repository is a fork of [Yerren/FreshWDL](https://github.com/Yerren/FreshWDL), maintained at [oe3gwu/FreshWDL](https://github.com/oe3gwu/FreshWDL).

**Current version:** 1.1.8.15 Alpha

**Live demo (upstream):** https://www.hackfarm.co.nz/FreshWDL/FreshWDL.html

## Features

- Live weather display from Weather Display **clientraw** files
- Animated gauges for temperature, wind, humidity, barometer, rainfall, solar, and UV
- Historical graphs (temperature, wind, rainfall, barometer, and more)
- Modal views for detailed graphs, records, and forecasts
- Multi-language interface (18 languages)
- Configurable units, gauges, graphs, and tooltips via `config.js`

## Requirements

- [Weather Display](https://www.weather-display.com/) uploading these files:
  - `clientraw.txt`
  - `clientrawextra.txt`
  - `clientrawhour.txt`
  - `clientrawdaily.txt`
- A web server to host the HTML page and configuration
- A modern browser with JavaScript enabled

## Quick Start

1. Clone this repository:

   ```bash
   git clone https://github.com/oe3gwu/FreshWDL.git
   ```

2. Edit `config.js` to match your station (file names, language, units). See [Configuration](#configuration).

3. Choose an HTML entry point and upload it together with `config.js` to your web server.

4. Make sure the clientraw files are reachable — either in the same directory as the HTML page, or via `customBaseURL` in `config.js`.

5. Open the HTML page in your browser.

## HTML Entry Points

| File | Description |
|------|-------------|
| `FreshWDLmaster.html` | Recommended template. Loads scripts and styles from jsDelivr CDN (`yerren/FreshWDL@master`). Only `config.js` needs to be hosted locally. |
| `FreshWDL.html` | Same CDN setup as above, with a custom page title. |
| `FreshWDLLayout02.html` | Alternative layout using `stylesheet02.css` and `InnerContent-02.js`. |
| `FreshWDLValidUnpublished.html` | Development template with mostly local assets (partial CDN for CreateJS, OpenTip, Chart.js). |

For a **fully local deployment** (e.g. offline networks or HAMNet), copy an HTML file and replace all CDN URLs with relative paths to the local `css/`, `js_bundles/`, and `sprites/` directories. `FreshWDLValidUnpublished.html` is a good starting point.

## Configuration

All user settings are in `config.js`:

| Setting | Description |
|---------|-------------|
| `clientRawName` etc. | Names of your clientraw files |
| `customBaseURL` | Optional base URL for clientraw files, e.g. `"http://example.com/wetter/"` (trailing slash required). Default: `false` |
| `lang` | Interface language (see [Languages](#languages)) |
| `generalSettings.tooltipsEnabled` | Enable or disable hover tooltips |
| `currentUnits` | Default display units on first load |
| `gaugeSettings` | Enable/disable gauges and set modes (solar, UV, wind chill, wind gust) |
| `graphSettings` | Enable/disable individual graphs |

Example — German language with tooltips disabled:

```javascript
lang = "de",
generalSettings = {
    tooltipsEnabled: false
},
```

Wind speed supports Beaufort scale: set `wind: "B"` in `currentUnits`.

## Languages

Set `lang` in `config.js` to one of:

`en`, `de`, `nl`, `da`, `ro`, `fr`, `gr`, `it`, `es`, `nb`, `bg`, `cs`, `fi`, `si`, `sv`, `pt`, `ca`, `hr`

Translations are maintained in `js_bundles/Globals.js`. The helper script `dictionaryAdder.py` can assist with adding new language entries.

## Project Structure

```
FreshWDL/
├── config.js                 # Your local configuration (upload to server)
├── FreshWDLmaster.html       # Recommended entry point
├── InnerContent.js           # Main widget layout
├── InnerContent-02.js        # Alternative layout
├── UpperContent.js           # Modal dialogs
├── css/                      # Stylesheets
├── js_bundles/               # Application logic and libraries
│   ├── Globals.js            # Translations and initialization
│   ├── WidgetsHandlers.js    # Widget and data handling
│   ├── Loading.js            # Loading screen
│   └── …                     # Chart.js, Moment.js, EaselJS, etc.
├── sprites/                  # UI images
├── Changelog.md              # Version history
└── LICENSE                   # GPLv3
```

## Troubleshooting

### Graphs show straight lines for 12-hour spans

The clientraw files are uploading in 12-hour format. Update Weather Display to a newer version.

### "Data Currently Unavailable" persists on the loading screen

- Verify clientraw file names in `config.js`
- Check `customBaseURL` if set
- Ensure the HTML page and `config.js` are in the same location as the clientraw files (when no custom URL is configured)
- Open the clientraw file URLs directly in the browser to confirm data is available

### Blank page or missing widgets

- Check the browser console for failed script or stylesheet loads
- When using CDN mode, ensure the server has internet access
- For local deployments, verify all paths in the HTML file point to existing local files

## Contributing

Bug reports and feature suggestions are welcome via [GitHub Issues](https://github.com/oe3gwu/FreshWDL/issues).

To contribute upstream, see [Yerren/FreshWDL](https://github.com/Yerren/FreshWDL).

## Credits

FreshWDL was created by **Yerren** ([yerren@renerica.com](mailto:yerren@renerica.com)).

- **Upstream:** https://github.com/Yerren/FreshWDL
- **This fork:** https://github.com/oe3gwu/FreshWDL
- **License:** GNU General Public License v3.0 (see [LICENSE](LICENSE))

## Donate

If this project has helped you, consider supporting the original author:

<a href='https://ko-fi.com/G2G6SUREK' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi5.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
