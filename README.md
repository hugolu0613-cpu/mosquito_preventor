# VectorMind v23.2 · AI 防蚊助手

This version puts the AI agent at the centre. The whole app is now **one chat screen**:

- **Status strip at the top:** risk ring, temperature and humidity, a mosquito-repellent button and a sighting-report button.
- **Chat with the AI agent:** it answers in Cantonese and shows **cards right inside the chat**, such as the risk breakdown, Hong Kong map, trend chart, 3-day forecast and sensors.
- **Device actions appear as "confirm" cards.** In Settings you can let the AI carry them out directly.
- **Suggestion chips:** situation now, Hong Kong map, next 3 days, trend, turn on repellent, dengue.
- **The agent speaks up first:** it sends a greeting when the app opens and a warning card when risk crosses your threshold.

## Map fix
The map no longer depends on Leaflet, CARTO or any map tile service, so it needs **no API key and no CDN**. The 18 districts and the network sensors are drawn by the app itself as SVG. Tap any district and the AI will analyse it.
Chart.js has also been removed; charts are now drawn on a canvas. Besides the data sources, the page doesn't load anything from the internet.

## Setup
1. Replace the whole `VectorMind` folder (`VectorMind.ino` and `page.h`), then compile and upload.
2. Open **http://vectormind.local** (or the IP address shown on Serial).
3. You can also open `vectormind.html` directly on your computer to try the demo mode.

AI: NVIDIA only (via the BlockPilot Worker; no key on the device or in the browser). Data: mp-supabase + Hong Kong Observatory.
After editing `vectormind.html`, run `python build_page.py` to regenerate `page.h`.

## v23.2 changes
- **502 "connection failed" fixed:** BearSSL's default 16 KB + 16 KB buffers used too much RAM. TX has been reduced to 512 bytes, which frees about 15 KB. When memory is too low, the device now returns a 507 error that shows the heap figures.
- **Fallback AI:** if NVIDIA fails, the app automatically switches to Pollinations (no key). It tries the browser first, then the device's `/api/poll`. Replies from the fallback are marked "後備 AI".
- **Full controls are back:** six tabs — AI Assistant (home), Overview, Map, Trend, Device, Settings. Every card has a "✨ 問 AI" button.
- **The map always shows:** if network data can't load, it uses estimates from the Observatory and your device.
- **Device → Diagnostics → "Test AI connection"** checks both NVIDIA and Pollinations.
