# IceSpotter – winter sidewalk hazard map for Riga

**IceSpotter** finds icy, snowy and wet sidewalks in Riga from camera photos and shows them on a map, so winter maintenance crews know where to go first.

Built at **RobotHack 2026** (Riga, 24–28 November 2026) for the challenge *PCH4 "Spot Winter Sidewalk Hazards"* by Rīgas pašvaldība (Riga City Council).

## How it works
1. **Capture** – a camera on a city vehicle (bus, sidewalk tractor) takes photos with GPS and time.
2. **Classify** – a small neural network (YOLO11n-cls) labels the sidewalk: `clear`, `wet`, `snow`, `ice` or `not_visible`.
3. **Score** – the risk score adds air temperature (wet at ≤ +2 °C → likely black ice), bridges, stairs, bus stops and model confidence.
4. **Dispatch** – a map of Riga with a Top‑10 list of places to send crews first, a "treated" button for contractor control and a CSV report.

## Results (honest)
- 95% accuracy on 65 new Riga street photos from districts the model never saw (previous version: 72%).
- 99% on ice images from the public Roads dataset.
- Few real Riga ice photos yet – that is the next step for a pilot.

## Run locally
```bash
pip install -r requirements.txt
streamlit run app.py
```

## Data and licences
- Street images: [Mapillary](https://www.mapillary.com), CC BY-SA 4.0
- Training data: Roads dataset (Jeswin Wilson, Roboflow Universe), CC BY 4.0
- Weather: Open-Meteo

**Live site:** https://icespotter.github.io

Team IceSpotter · RTU, Riga, Latvia
