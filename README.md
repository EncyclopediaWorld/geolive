# GeoLive · Geographic Intelligence Dashboard 🌍

[![HTML5](https://img.shields.io/badge/HTML5-Canvas-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-199900?logo=leaflet&logoColor=white)](https://leafletjs.com/)
[![License: Apache 2.0](https://img.shields.io/badge/Code-Apache_2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![License: CC BY 4.0](https://img.shields.io/badge/Content-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
![GitHub Forks](https://img.shields.io/github/forks/EncyclopediaWorld/geolive?style=flat)
[![GitHub stars](https://img.shields.io/github/stars/EncyclopediaWorld/geolive?style=social)](https://github.com/EncyclopediaWorld/geolive)
[![GitHub downloads](https://img.shields.io/github/downloads/EncyclopediaWorld/geolive/total?color=brightgreen&label=Downloads)](https://github.com/EncyclopediaWorld/geolive/releases)
[![Layers](https://img.shields.io/badge/Data_Layers-17-38bdf8)]()
[![APIs](https://img.shields.io/badge/Live_APIs-12+-34d399)]()
![Visitors](https://visitor-badge.laobi.icu/badge?page_id=EncyclopediaWorld.geolive)

> **The entire living Earth in your browser.**

GeoLive transforms your browser into a real-time geographic intelligence command center. Just open it and watch the planet breathe.

---

## ✨ Why GeoLive?

Ever wished you could glance at one screen and instantly see the temperature, wind, rain, waves, air quality, wildfires, droughts, and population density of **any place on Earth** — all at once, all in real time?

That's GeoLive. It pulls from **12+ live public APIs** and renders **17 toggleable data layers** onto a gorgeous dark-mode map, complete with adaptive canvas overlays, interpolated grids, and smooth glassmorphism UI.

---

## 🗂️ Layer Catalog

### 🌦️ Weather
| Layer | Source | Description |
|-------|--------|-------------|
| **Precipitation** | RainViewer | Live radar mosaic — rain, snow, hail in real time |
| **Air Temperature** | Open-Meteo | 16×16 interpolated grid with Gaussian-blurred canvas heatmap for smooth gradients |
| **Wind** | Open-Meteo | Beaufort-scaled arrow field showing speed & direction |
| **Satellite Cloud** | NASA VIIRS | True-color corrected reflectance imagery |

### 😷 Air Quality
| Layer | Source | Description |
|-------|--------|-------------|
| **Air Quality (AQI)** | Open-Meteo | 8×8 PM2.5 heatmap with US AQI color scale |

### 🌊 Ocean & Marine
| Layer | Source | Description |
|-------|--------|-------------|
| **Tides & Waves** | Open-Meteo Marine + Natural Earth | Global coastlines colored by wave height — bright blue = high, dim blue = low — with mini range bars showing position in local min–max |
| **Sea Surface Temp** | GHRSST / NASA GIBS | MUR L4 + G1SST via WMS with multi-date fallback (3–7 day lag compensation) |
| **Sea Marks** | Marine Regions + OpenSeaMap + NOAA ENC | EEZ boundaries, IHO sea areas, continental shelves, nautical navigation marks, and US chart data — visible at any zoom level |

### 🌿 Land & Ecology
| Layer | Source | Description |
|-------|--------|-------------|
| **Vegetation (NDVI)** | NASA MODIS Terra | 8-day composite normalized vegetation index |
| **Land Surface Temp** | NASA MODIS | Daytime thermal emission |
| **Drought / Soil** | Open-Meteo | 16×16 two-layer soil moisture (0–7 cm + 7–28 cm) with Gaussian-blurred drought color mapping |

### ⚠️ Hazards
| Layer | Source | Description |
|-------|--------|-------------|
| **Disaster Alerts** | NWS + USGS + NASA EONET + GDACS | Active warnings — tornado, flood, earthquake (M3+), volcanic eruptions, wildfires, icebergs, and global natural events |
| **Fire Hotspots** | NASA VIIRS + MODIS | VIIRS SNPP 375m day/night thermal anomalies + MODIS Terra/Aqua WMS for broad coverage |

### 🏙️ Urban
| Layer | Source | Description |
|-------|--------|-------------|
| **Night Lights** | VIIRS Black Marble | Global light pollution visualization |
| **Population Density** | SEDAC GPWv4 | Triple-fallback WMS (NASA Disasters MapServer → GIBS → SEDAC ImageServer) |

### 🗺️ Base Maps
| Layer | Source | Description |
|-------|--------|-------------|
| **Satellite Imagery** | ESRI World Imagery | High-res photographic basemap |
| **Roads** | OpenStreetMap | Street-level reference overlay |

---

## 🎯 Feature Highlights

- **🔴 Live GPS positioning** — auto-detects your location with pulsing blue marker
- **📊 Real-time info cards** — temperature, wind, waves, AQI displayed in floating panels with mini sparkline bars
- **🎨 Canvas-rendered overlays** — temperature, wind, drought, and AQ drawn pixel-by-pixel with bilinear interpolation across a 16×16 grid, then Gaussian-blurred for seamless gradients
- **🌊 Global coastal tide visualization** — every coastline on Earth traced in blue, with brightness mapping wave height and periodic mini range bars
- **⚓ Multi-source maritime layer** — EEZ boundaries + IHO sea areas + continental shelves + OpenSeaMap buoys/lights + NOAA ENC charts
- **📱 Fully responsive** — desktop, tablet, mobile, iOS safe-area aware
- **🌙 Dark mode native** — deep navy glassmorphism UI with backdrop-filter blur
- **⚡ Lazy loading** — layers only fetch data when toggled on
- **🔄 Auto-refresh** — weather data refreshes every 10 minutes, grid data re-fetches on map move
- **🛡️ Multi-CDN resilience** — coastline data tries GitHub → jsDelivr → unpkg → npmmirror, with marine-grid auto-generation as last-resort fallback
- **📦 Batched API requests** — weather grid split into 128-point batches for reliability with `best_match` model selection

---

## 🚀 Quick Start

```bash
# Clone it
git clone https://github.com/EncyclopediaWorld/geolive.git

# Open it — that's it!
open geolive/geomap.html
```

Or just download the HTML file and double-click. No `npm install`, no `docker compose`, no environment variables. It's one file.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│                geomap.html (single file)        │
├──────────┬──────────┬───────────────────────────┤
│  Leaflet │  Canvas  │    Glassmorphism UI       │
│  Map +   │  Overlay │  Sidebar · Info Cards     │
│  Tiles   │  Engine  │  Legend · Toast · FAB      │
├──────────┴──────────┴───────────────────────────┤
│              Live Data Fetchers                  │
├────┬────┬─────┬──────┬─────┬─────┬────┬────────┤
│Open│Rain│NASA │Marine│NOAA │NWS  │USGS│  GDACS │
│Meteo│View│GIBS│Regions│ENC │+EONET│    │        │
├────┴────┴─────┴──────┴─────┴─────┴────┴────────┤
│  OpenSeaMap · SEDAC · ESRI · CARTO · OSM        │
└─────────────────────────────────────────────────┘
```

Everything lives in a single `<script>` block. No frameworks, no bundlers, no dependencies beyond Leaflet (loaded from CDN). The canvas overlay engine supports both static (`CanvasOverlay`) and animated (`AnimOverlay`) rendering modes with automatic repositioning during map pan/zoom.

---

## 📡 Data Sources & Attribution

| Provider | Layers | License |
|----------|--------|---------|
| [Open-Meteo](https://open-meteo.com/) | Weather, Marine, Air Quality | CC BY 4.0 |
| [NASA GIBS](https://earthdata.nasa.gov/gibs) | VIIRS, MODIS, GHRSST | Public Domain |
| [NASA EONET](https://eonet.gsfc.nasa.gov/) | Global Natural Events (volcanoes, storms, wildfires) | Public Domain |
| [RainViewer](https://www.rainviewer.com/) | Precipitation Radar | Free tier |
| [Natural Earth](https://www.naturalearthdata.com/) | Coastline Geometry | Public Domain |
| [Marine Regions (VLIZ)](https://www.marineregions.org/) | EEZ, IHO Sea Areas, Continental Shelves | CC BY 4.0 |
| [OpenSeaMap](https://www.openseamap.org/) | Nautical Marks | CC BY-SA 2.0 |
| [NOAA Chart Display](https://nauticalcharts.noaa.gov/) | US ENC Nautical Charts | Public Domain |
| [NWS](https://www.weather.gov/) | Weather Alerts (US) | Public Domain |
| [USGS](https://earthquake.usgs.gov/) | Earthquake Data (M3+, global) | Public Domain |
| [GDACS](https://www.gdacs.org/) | Disaster Alerts (global) | Public |
| [CARTO](https://carto.com/) | Dark Basemap | CC BY 3.0 |
| [ESRI](https://www.esri.com/) | Satellite Imagery | ESRI Master License |
| [SEDAC / CIESIN](https://sedac.ciesin.columbia.edu/) | Population Density | NASA EOSDIS |

---

## 🤝 Contributing

Found a bug? Want to add a new layer? PRs are welcome!

```bash
# It's just one HTML file — fork, edit, submit.
```

Ideas for new layers: ocean currents, lightning, UV index, snow cover, real-time flight paths, marine traffic (AIS)...

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=EncyclopediaWorld/geolive&type=Date)](https://star-history.com/#EncyclopediaWorld/geolive&Date)

---

## 📄 License

Code: [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) — Content & visualizations: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

---

<p align="center">
  <b>🌍 One file. Seventeen layers. One living planet.</b><br>
  <sub>Built with 💙 and public data</sub>
</p>
