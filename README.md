# IceSpotter – winter sidewalk hazard map for Riga

**IceSpotter** finds snow and ice on Riga sidewalks from camera photos and the weather forecast, and shows winter maintenance crews where to clean first.

Built at **RobotHack 2026** (Riga, 24–28 November 2026) for the challenge *PCH4 "Spot Winter Sidewalk Hazards"* by Rīgas pašvaldība (Riga City Council).

## How it works
1. **Capture** – a phone or small camera on vehicles that already drive: city buses find problems, the sidewalk cleaning machines confirm the result. One frame every few seconds with GPS and time.
2. **Classify on the device** – a small neural network (YOLO11n-cls, 6 MB, runs in the browser with onnxruntime-web) labels the frame: `ice`, `snow`, `wet`, `clear`, `blocked` or `not_visible`. Only the result and a small cropped, blurred photo are sent; no video is stored.
3. **Prioritise** – risk points for ice and snow, public transport stops (1,652 Rīgas satiksme stops), bridges, places not cleaned since yesterday and places still icy after they were marked "treated".
4. **Dispatch and check** – a map of Riga with all places ranked by risk, a crew route by real streets (OSRM), a "treated" button, a re-check when a camera passes again, and a weather-based ice risk for tonight (Open-Meteo).

## Results (honest)
- Model recipe, 4-fold check on 682 hand-labelled Riga photos (test photos never used for training): 89% accuracy over 6 classes, 91% of snow found, 1% false hazards on clear or wet sidewalks.
- Model v8 on 38 web photos of icy or snowy sidewalks it never saw (2-fold): 30 of 38 flagged as a hazard, 17 of 32 ice photos labelled as ice (v7: 3 of 32).
- Night black ice (Zenodo set, unseen): 86%.
- Weak spots: thin clear ice can look wet, thick ice crust is sometimes called snow, the camera needs light at night, and there are few real ice photos from Riga yet – that is the next step for a pilot.

## Data and licences
- Street images: [Mapillary](https://www.mapillary.com), CC BY-SA 4.0
- Roads dataset (Jeswin Wilson, Roboflow Universe), CC BY 4.0
- Black ice outdoor set, Zenodo record 10428765, CC BY 4.0
- Public transport routes and stops: Rīgas satiksme GTFS, data.gov.lv, CC0
- Weather: Open-Meteo · Routing: OSRM / OpenStreetMap

## Pages
- `index.html` – dispatcher map, risk list, crew route, demo drive, photo check
- `camera.html` – phone camera module (add `?demo` for an indoor demo without GPS)

**Live site:** https://icespotter.github.io

Team IceSpotter · RTU, Riga, Latvia
