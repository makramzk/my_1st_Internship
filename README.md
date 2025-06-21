# 🏞️ Berlin Parks & Playgrounds Data Layer
This project focuses on modeling, transforming, and integrating data related to **parks and playgrounds in Berlin**. It is part of a broader effort to map and enrich recreational zones across the city, enabling better insights for urban planning, public services, and neighborhood enrichment.

## 📌 Project Overview
We follow a three-step workflow:

Research & Data Modelling

Data Transformation

Database Population

The focus is currently on two types of recreational zones:

Public Parks (Grünanlagen)

Playgrounds (Spielplätze)

🧪 Step 1: Research & Data Modelling
Branch Name: layer-data-modelling

1.1 Data Source Discovery
We identified two key datasets from the Berlin city government's official portal:

🟢 Public Parks (Grünanlagen)
Source: Berlin Open Data - Parks Layer

Origin: Berlin Senate Department for Urban Development

Update Frequency: Unknown (likely updated periodically)

Data Type: Static (available as downloadable GIS files)

🛝 Playgrounds (Spielplätze)
Source: Berlin Open Data - Playgrounds Layer

Origin: Berlin Senate Department for Urban Development

Update Frequency: Unknown

Data Type: Static

1.2 Modelling & Planning
Key Parameters Selected:

Name

Type

Address

District

Coordinates (latitude, longitude)

Area/Size

Facilities (for playgrounds)

Opening hours (if available)

Schema Integration Plan:

Link new data to existing neighborhoods and listings tables using coordinates and district names.

Draft Schema:

sql
Copy
Edit
parks_and_playgrounds (
  id SERIAL PRIMARY KEY,
  name TEXT,
  type TEXT,
  address TEXT,
  district TEXT,
  latitude FLOAT,
  longitude FLOAT,
  area FLOAT,
  facilities TEXT,
  source TEXT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)
Known Data Issues:

Inconsistent or missing names

Lack of standardized district naming

Variability in GPS accuracy

Transformation Plan:

Normalize names and types

Clean GPS data

Standardize district fields to match internal database

Convert coordinate system if needed (from EPSG:25833 to WGS84)

1.3 /sources Directory
Raw data files and metadata are included in the /sources folder.

See /sources/README.md for:

Source descriptions

Planned transformation steps

🔄 Step 2: Data Transformation
Branch Name: parksandrecs-data-transformation

Python or SQL scripts for data transformation are in the /scripts directory.

Includes:

Schema mapping

Cleaning operations

Format normalization

Coordinate transformation

This step does not involve database insertion.

All outputs are tested locally and validated against the planned schema.

🗄️ Step 3: Database Population
Branch Name: parksandrecs-populating-db

Inserts transformed data into the database.

Schema setup and table creation based on Step 1.

Establishes foreign keys and joins to listings or neighborhood entities.

Includes verification steps.

(Optional) GitHub Actions are configured for future automation if data becomes dynamic.

📂 Repository Structure
bash
Copy
Edit
├── sources/
│   ├── README.md         # Data source info & transformation steps
│   └── *.geojson / *.xml # Raw data files
│
├── scripts/
│   └── transform_parks_playgrounds.py  # Data cleaning and schema mapping logic
│
├── README.md             # Project overview and documentation
📬 Contributing
Please follow branch naming conventions and PR submission for each step. Review all changes before merging to main.
