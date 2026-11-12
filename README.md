# Brilliant Hunter — Build 03

## What this build does
- Loads public Chess.com archives for a username (default: mossfeast).
- Parses PGN game records.
- Provides a Stockfish Web Worker integration.
- Runs a basic candidate-scan: it checks whether the played move matches Stockfish's top move, then whether the engine's best reply appears to capture the moved piece.

**Important:** the candidate scan is only a crude Brilliant-like heuristic. It is not Chess.com's official classifier, and it can miss sacrifices or produce false positives. It does not calculate Chess.com's official label.

## Required Stockfish engine files
The ZIP does not contain the engine binaries. Download the matching Stockfish.js v19.0.1 lite single-thread files and place them in the same folder as `index.html`:

- `stockfish-19-lite-single.js`
- `stockfish-19-lite-single.wasm`

Direct upstream package URLs:
- https://cdn.jsdelivr.net/npm/stockfish@19.0.1/bin/stockfish-19-lite-single.js
- https://cdn.jsdelivr.net/npm/stockfish@19.0.1/bin/stockfish-19-lite-single.wasm

The official Stockfish.js package documents that the browser Worker loads the matching WASM file from the same directory. The lite single-thread build is about 1.7 MB and does not require cross-origin isolation headers.

## Run on iPad
1. Extract this ZIP.
2. Download both engine files above into the extracted folder (same level as index.html).
3. Host the folder on an HTTPS static host. A service worker and Worker require a secure origin; opening index.html directly from Files is not enough.
4. Open the HTTPS URL in Safari, then Share → Add to Home Screen.

## Known limitations
- This is a prototype; iPad Safari execution has not been tested in this environment.
- The first scan checks depth 10 and can take time. Test one game first.
- Chess.com may rate-limit archive requests.
- Public game history only; no password or account login is needed.
- Stockfish.js is GPL-3.0. Keep its licence and corresponding source notices with redistributed copies.
