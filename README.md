# fitparserx library

A lightweight Python library for parsing Garmin .fit files and extracting wellness data (heart rate, stress level, respiration rate) into convenient Python structures (pandas DataFrame, NumPy array). These data are sourced from Garmin Wellness exports: either the daily export (Account Settings > Account Information > Export Wellness Data) or the full archive emailed via the [Data Management](https://www.garmin.com/en-US/account/datamanagement/) page. Support for Garmin activity data will be added in a future release.

## Features

Uses Garmin .fit files decoded with the garmin_fit_sdk to:
- Extract proper datetimes and heart rate data.
- Optionally include respiration rate and stress level data.
- Converts the raw data into a pandas DataFrame or a NumPy array.
- Timezone‑aware datetime handling.

## Installation

1. (Optional) Create and activate a virtual environment:
```
python3 -m venv .venv
source .venv/bin/activate
```
2. Install the package using pip:
```
pip install fitparserx
```

## Usage

from fitparserx import FitParser

### Initialize parser pointing to a directory or single file
Put your data into a data/ file. Otherwise, the parser goes through
data in the current working directory. You can also point a path to a specific file.

mode='all' requires `email` prefix for .fit filenames
```
parser = FitParser(path="./data", email="user@example.com", mode="all")
```

### DataFrame
Convert to a pandas DataFrame with datetimes and metrics:
```
# Only heart rate (default)
fit_df = parser.to_dataframe()

# Include stress level and respiration rate, fill missing with NaN
fit_df = parser.to_dataframe(add_metrics=["stress_level", "respiration_rate"], timezone="UTC")
```

### NumPy Array
```
fit_np = parser.to_numpy()
```

### License

MIT License
