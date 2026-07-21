# FIRST/STRIKE

**A rapid initial attack dispatch prototype — the missing connection between fire detection and fire response.**

Almost every catastrophic wildfire was once a small fire. Satellites already spot new ignitions within minutes, and the world is already full of aircraft and airfields — but nothing connects detection to response. First Strike is a working, single-file demonstration of that missing layer: it shows every wildfire burning on Earth right now, how long it has burned, and how fast help *could have* arrived.

Open `first-strike-dispatch.html` in a browser. No build, no server, no API keys.

## What it shows

Every fire in the list carries a live **T+ clock** — time since satellite detection — color-coded against a first-hour containment window. Click a fire and the tool computes the nearest airfield, the estimated response time, and scans the actual sky for the nearest real aircraft that could divert. Press **SIMULATE RESPONSE** and watch the race: a tanker scrambling from the base versus a real, named flight diverting from its live position.

The gap between "help could arrive in ~40 minutes" and "this fire has burned for 80 days with no response" is the entire argument.

## Levers

| Lever | What it does |
|---|---|
| **SATELLITE** | Overlays NASA true-color imagery (GIBS) of the whole planet |
| **3D TERRAIN** | Real elevation mesh + WebGL hillshade relief; fires sit *in* terrain |
| **ALL AIRFIELDS** | Swaps the curated demo network for all 5,276 medium/large airports on Earth and recomputes every metric — the "every airport is a fire station" scenario |
| **LIVE AIRCRAFT** | Real planes overhead now, via community ADS-B feeds |
| **WIND** | Animated wind forecast (Windy embed) at the map center |
| **LIVE TV** | Multiview news wall with channel picker and dead-stream auto-swap |

The **INSIGHTS** tab charts where the world is burning by region and what share of each region's fires could have help within the first hour — the coverage-gap chart that makes the case for the network.

## The concept stack

1. **Detect** — subscribe to satellite ignition feeds (EONET today; FIRMS/FireSat-class constellations next). Detection is effectively solved.
2. **Dispatch** — automated event-to-launch decisioning: which asset, from where, arriving inside the containment window. This repo is a sketch of that layer.
3. **Contain** — deliver suppressant while the fire is small. The physics: gallons per minute per dollar, inside the window, per square mile of coverage.

### The Magic Carpet

A concept for turning the aircraft already in the sky into first responders: a conformal belly pod — a *soft chemical carpet* — strapped to the underside of a participating airframe and deployed remotely once government-approved satellite dispatch systems align (verified ignition, cleared geometry, authorized release). The release is engineered to be safe for people and habitat: a wide, low-energy dispersal that blankets a line rather than a blast.

Payload scales with the airframe, so protective capacity can be computed per aircraft — the prototype does exactly this, estimating pod size from each real aircraft's ADS-B size category and translating it into feet of protective line. The doctrine is two-stage guardianship: the diverting aircraft lays a **protective shield line** to safeguard people, homes, and habitat in the first minutes, buying time for a larger automated tanker drone launching from the nearest airfield to follow up, fully extinguish the fire, and leave the land safe.

The bigger idea: an opt-in **Civil Fire Reserve** — like the Civil Reserve Air Fleet, but for fire — where ag aviation, general aviation, and cargo operators carry certified suppression pods and get tasked through the dispatch layer.

## Live data sources (all free)

- **NASA EONET** — open wildfire events (curated; North-America-leaning; FIRMS integration planned for full global hotspots)
- **NASA GIBS / Worldview Snapshots** — satellite imagery layers and per-fire thumbnails
- **OurAirports** (public domain) — the worldwide airfield network
- **adsb.lol / airplanes.live / adsb.fi** — community ADS-B live aircraft (auto-rotating provider chain)
- **AWS/Mapzen terrain tiles** — elevation for 3D and hillshade
- **OpenStreetMap / CARTO** — basemaps · **Nominatim** — place search
- **Windy.com / YouTube** — embedded wind and live TV

## Honest assumptions (demo, not doctrine)

Response modeling uses illustrative heuristics: 12-minute scramble, 140 kt cruise, a 60/180-minute containment window, 2-minute airborne divert decision, and Magic Carpet pod sizes by ADS-B category (60–2,000 gal) at ~3 ft of retardant line per gallon. Fire locations, detection times, imagery, airfields, and aircraft positions are real. Nothing here claims every fire is stoppable — some long-burners are managed intentionally or unreachable by any first strike. The claim is narrower and harder to argue with: **most of them never even got the chance.**

**Cost estimates** shown on each fire are anchored to published figures rather than invented: retardant ≈ $3/gal ([RAND economist Edward Keating](https://www.frontlinewildfire.com/wildfire-news-and-resources/aerial-wildfire-fighting-how-effective-is-it/), with USFS contract ranges of roughly $2–5/gal per [Wildfire Today](https://wildfiretoday.com/how-much-does-it-cost-to-drop-retardant-on-a-fire/)); heavy air tanker operations "upwards of $6,000/hr" (RAND, same source); and $2,000 per plane-hour for the crop-duster class — the actual rate [Saskatchewan's provincial SEAT program bills](https://globalnews.ca/news/4255446/saskatchewan-municipalities-firefighting-crop-dusters/amp) for ag aircraft on fire duty, a working government precedent for exactly the network this project envisions. The contrast that makes the model matter: aggressive initial attack historically runs **$10k–$75k per fire**, while a large fire that escapes runs **$30–50M to suppress** ([Wildfire Today](https://wildfiretoday.com/the-cost-of-saving-money-on-wildfire-suppression-2/)) — before counting property losses that can reach hundreds of millions. Every dispatch estimate in the app is a rounding error against one escape.

## Roadmap

- FIRMS raw-hotspot lever (free NASA key) with clustering — the true global detection picture
- Real ag-operator and tanker-base dataset to replace the demo network
- Suppression-demand model: fuel, weather, terrain → gallons-within-minutes requirements
- Port into a proper mapping platform as a standing dispatch layer

## Author

**Joshua A. Talbott, M.Tech.** — Director of Technology, Kent State University College of Sciences and Humanities. Master's in Technology from what is now Kent State's College of Aeronautics and Engineering; has taught computer manufacturing for that college. Drone pilot from a family of aviators. This project is where the two threads of his career — manufacturing technology and aviation — meet in service of the public.

*Demonstration software. Not an operational dispatch system. Verify everything against the live-source links built into every fire.*
