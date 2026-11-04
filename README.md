# RapidGo — Chance-O-Meter

A map-centred commute interface for Delhi-NCR, built with a liquid-glass visual style. Explore pickup locations, compare illustrative ride fares, and try a journey flow that introduces alternative pickups and a metro option.

**Current status: interactive frontend prototype.** This repository contains a standalone HTML application. Matching scores, Captain activity, traffic labels and booking transitions are demonstrations; they are not connected to a live ride-hailing service.

## Features

- Interactive Leaflet map with street and satellite layers.
- Pickup and destination selection through map clicks and draggable markers.
- Swap pickup and destination, recenter the map, and request browser GPS access.
- Chance-O-Meter display with pickup factors and an illustrative matching score.
- Bike and auto fare cards that update when coordinates change.
- Alternative pickup selection with a walking-line visual.
- Metro station marker and a metro selection interaction.
- Demonstration flow for selecting a ride, searching, matching, completing a trip and viewing a receipt.
- Responsive layout, bottom sheets, status notifications and a live clock.

## Run locally

No package installation, build step or API keys are required for this prototype. An internet connection is needed to load the CDN libraries, fonts and map tiles.

```bash
git clone https://github.com/STUCKINLOOP8/chance-O-meter.git
cd chance-O-meter
python -m http.server 8000
```

Open **http://localhost:8000** in your browser. On systems that expose Python as `python3`, use `python3 -m http.server 8000` instead. Stop the server with `Ctrl+C`.

You can also open `index.html` directly for a quick preview. A local web server is preferable for browser permissions. GPS requires permission and a browser environment that supports geolocation; hosted deployments normally require HTTPS.

## Try the interface

1. Choose pickup or destination mode, then click the map or drag its markers.
2. Swap the two locations or use the GPS control to choose your current position.
3. Review the updated illustrative fare, duration and Chance-O-Meter display.
4. Select the bike booking action to enter the demonstration search flow.
5. Try the alternative pickup action to see the pickup move and the simulated matching transition.
6. Select the metro option to focus its station marker, or complete the demonstration trip to view the receipt.

Typing an address does not perform geocoding. Use map coordinates or GPS to change the actual location. The initial scene uses sample locations around Connaught Place and Gurugram.

## What the prototype calculates

| Display | Current implementation |
| --- | --- |
| Matching score | Rules based on pickup-name keywords and a coordinate-derived fallback; not a calibrated probability |
| Trip distance | Haversine distance multiplied by 1.25, with a minimum-distance rule; not a road-network route |
| Journey duration | Assumed speeds and peak-hour rules based on the browser's local clock; no observed traffic |
| Fares | Client-side distance rates, a time-of-day multiplier and a base fare; not a provider quote |
| Walking and trip lines | Polylines between selected coordinates; not verified walking or driving directions |
| Captain markers and matching | Sample coordinates, animated activity and scripted transitions; no live dispatch |
| Metro option | A sample station interaction; no timetable, live arrivals, fare verification or ticket booking |
| Receipt | A demonstration fare breakdown; no payment has been processed |

The call and safety buttons currently display notifications. They do not place calls, contact emergency services or send alerts.

## Technology and project structure

The application uses HTML, inline CSS, vanilla JavaScript, Tailwind CSS 3.4.17 through its CDN, Leaflet 1.9.4, and the Plus Jakarta Sans Google Font. Street tiles come from OpenStreetMap and satellite imagery from Esri's World Imagery endpoint.

```text
chance-O-meter/
├── index.html   # Complete interface, styling, map setup and demo logic
└── README.md    # Setup, behaviour and implementation status
```

There is no backend, database, authentication system, server configuration or persistent booking history in this repository. Reloading the page resets its in-memory state.

## Customization

Edit `index.html` to change the interface and demonstration settings:

- `FARE_CONFIG`: bike/auto distance rates and the base fare.
- `pickupCoords` and `dropCoords`: initial journey coordinates.
- `CAPTAINS_DATA`: sample Captain marker positions.
- `calculateProbabilityForPickup()`: illustrative matching-score rules.
- `evaluateTraffic()`: assumed peak-hour multipliers and speeds.
- `initMap()`: map layers, markers and interactions.
- CSS classes and inline templates: branding, glass effects and responsive layout.

## Static hosting

The app can be served by a static web host. To configure GitHub Pages, open this repository's **Settings → Pages**, choose deployment from the `main` branch and `/ (root)`, then save. This describes the setup; Pages has not been enabled or verified as part of the source push.

Before publishing, add visible map-provider attribution: the current map initialization disables Leaflet's attribution control. Review the requirements for both tile providers and use a production CSS build rather than Tailwind's browser CDN for a production release.

## Work needed for a real service

- Server-side authentication, authorization and persistent accounts/trips.
- Real Captain onboarding, approval, location updates and atomic dispatch.
- Road and walking routing, address search and verified pickup-access data.
- Evidence-backed matching assessment, outcome collection and model calibration.
- Licensed transit schedules, complete itineraries and a supported ticketing integration if required.
- Server-generated quotes, trip OTP verification and payment-provider verification.
- Real safety/support integrations, network recovery, accessibility review and device testing.

No automated test suite is included. The inline JavaScript syntax was checked before the initial HTML push; complete browser, device and integration testing remains outstanding.

## License

No project license has been selected in this repository. Third-party libraries, fonts, map data and imagery remain subject to their respective terms and attribution requirements.
