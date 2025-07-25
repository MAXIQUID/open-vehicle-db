Here’s a draft README.md tailored for integrating the open_vehicle_db module into OEM.autos, reflecting its role as a vehicle selection service powering Year → Make → Model → Style logic across your stack:

⸻

🧠 OEM.autos Vehicle DB Module

This module provides a unified vehicle hierarchy interface (Year → Make → Model → Style) to power part lookup, fitment validation, and FOE (Factory Original Equipment) structuring across the OEM.autos ecosystem.

It integrates with the open_vehicle_db dataset, which includes:
	•	✅ 69 makes (e.g., Toyota, Ford)
	•	✅ 1,678 models (e.g., Prius V, F-150)
	•	✅ 9,730 styles (e.g., PRIUS V 5DR HATCHBACK)
	•	✅ Coverage from 1981 through 2026 (Last updated: Feb 21, 2025)

⸻

🚀 What This Powers
	•	🔎 Search filters on part scrapers
	•	📦 FOE JSON schema (vehicle context for part listings)
	•	🧩 VIN / VDS resolution (planned)
	•	🌐 Frontend dropdown selectors (vehicle pickers)

⸻

📦 Installation

Clone the forked repo and install in editable mode:

git clone https://github.com/your-username/open_vehicle_db.git
cd open_vehicle_db
pip install -e .

Or embed directly in your oem.autos/modules/ folder.

⸻

🧩 Usage (Python)

from oem.autos.api import vehicle_db

# List all supported years
vehicle_db.get_years_supported()

# Get makes for a year
vehicle_db.get_makes(2003)

# Get models for a specific make and year
vehicle_db.get_models(2003, "Mazda")

# Get all available styles for a vehicle
vehicle_db.get_styles(2003, "Mazda", "Protege")


⸻

🛠 API Routes (if using FastAPI)

GET /api/vehicle/years
GET /api/vehicle/makes?year=2003
GET /api/vehicle/models?year=2003&make=Mazda
GET /api/vehicle/styles?year=2003&make=Mazda&model=Protege


⸻

🧱 Example Output (Used in FOE)

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


⸻

🧠 Future Plans
	•	🔗 VDS-based prefill and VIN decoding
	•	🧠 Fuzzy matching for style validation during scraping
	•	💾 SQLite pre-cache for offline + fast local queries
	•	🌍 International vehicle DB merging (EU, JDM, LHD/RHD)

⸻

🧑‍💻 Repo Structure

oem.autos/
├── api/
│   └── vehicle_db.py        ← Adapter layer
├── modules/
│   └── open_vehicle_db/     ← Forked or vendorized dataset
└── ...


⸻

📜 License

MIT — Same as open_vehicle_db

⸻

Would you like me to also generate a docs/ folder with OpenAPI schema or UI mockup for the dropdown selector?