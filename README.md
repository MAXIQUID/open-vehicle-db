# 🧠 OEM.autos Vehicle DB Module

This module provides a unified vehicle hierarchy interface (Year → Make → Model → Style) to power part lookup, fitment validation, and FOE (Factory Original Equipment) structuring across the `OEM.autos` ecosystem.

It integrates with the `open_vehicle_db` dataset, which includes:

- ✅ 69 makes (e.g., `Toyota`, `Ford`)
- ✅ 1,678 models (e.g., `Prius V`, `F-150`)
- ✅ 9,730 styles (e.g., `PRIUS V 5DR HATCHBACK`)
- ✅ Coverage from 1981 through 2026  
- 📅 Last updated: February 21, 2025

---

## 🚀 What This Powers

- 🔎 Search filters on part scrapers
- 📦 FOE JSON schema (vehicle context for part listings)
- 🧩 VIN / VDS resolution (planned)
- 🌐 Frontend dropdown selectors (vehicle pickers)

---

## 📦 Installation

```bash
git clone https://github.com/your-username/open_vehicle_db.git
cd open_vehicle_db
pip install -e .
```

Alternatively, copy the module directly into `oem.autos/modules/` if preferred for tight integration.

---

## 🧩 Usage

```python
from oem.autos.api import vehicle_db

# List all supported years
years = vehicle_db.get_years_supported()

# Get makes for a specific year
makes = vehicle_db.get_makes(2003)

# Get models for a year/make combo
models = vehicle_db.get_models(2003, "Mazda")

# Get styles for a year/make/model
styles = vehicle_db.get_styles(2003, "Mazda", "Protege")
```

---

## 🛠 FastAPI Routes

```http
GET /api/vehicle/years
GET /api/vehicle/makes?year=2003
GET /api/vehicle/models?year=2003&make=Mazda
GET /api/vehicle/styles?year=2003&make=Mazda&model=Protege
```

---

## 🧱 Example Output (FOE Schema)

```json
{
  "vehicle": {
    "year": 2003,
    "make": "Mazda",
    "model": "Protege",
    "style": "PROTEGE 4DR SEDAN LX/ES 2.0L"
  },
  "parts": [
    {
      "part_number": "BP4W-13-215A",
      "group": "Fuel System",
      "description": "Fuel Injector",
      "price": 84.99
    }
  ]
}
```

---

## 🧠 Future Plans

- 🔗 VDS-based prefill and VIN decoding
- 🧠 Fuzzy matching for style validation during scraping
- 💾 SQLite pre-cache for offline + fast local queries
- 🌍 Merge with EU/JDM/global vehicle schemas (support LHD/RHD)
- 📦 Graph traversal to identify compatible siblings / trims

---

## 📁 Repo Structure

```text
oem.autos/
├── api/
│   └── vehicle_db.py         # Adapter layer (vehicle → FOE logic)
├── modules/
│   └── open_vehicle_db/      # Forked or vendorized source dataset
└── ...
```

---

## 📜 License

MIT — Same license as `open_vehicle_db`