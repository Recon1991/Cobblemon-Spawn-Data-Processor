# Cobblemon Spawn Data Extractor

## Overview
The Cobblemon Spawn Data Extractor is a Python script designed to extract and analyze Pokémon spawn data from cobblemon JSON files. This project allows you to efficiently process, extract, and organize spawn information into a CSV format for easier analysis and reference.

### Features
- Extracts Pokémon spawn and species data from `.zip` and `.jar` archives containing JSON files.
- Outputs a detailed CSV file with information on Pokémon species, spawn conditions, egg groups, biomes, moon phases, and more.
- Supports a "Fun Mode" that adds colorful terminal outputs using `colorama`.
- Processes data in-memory to optimize for speed.
- Uses concurrency to improve extraction and processing efficiency.

## Prerequisites
- Python 3.7+
- Required Python packages:
  - `aiofiles`
  - `colorama`
  - `asyncio`

To install the required packages, run:
```bash
pip install -r requirements.txt
```

## Configuration
The script uses a configuration file `config.json` to set key parameters such as:
- `ARCHIVES_DIR`: Directory containing `.zip` or `.jar` files.
- `output_filename`: Filename for the generated CSV file.
- `skipped_entries_filename`: Filename for entries that do not have spawn data.
- `MAX_WORKERS`: Maximum concurrent threads used for extraction.
- `LOG_FILENAME`: Filename for log output.
- `LOG_LEVEL`: Logging level (e.g., `INFO`, `DEBUG`).
- `FUN_MODE`: Enable or disable fun-colored terminal outputs (`true` or `false`).

Example `config.json`:
```json
{
  "ARCHIVES_DIR": "./archives",
  "output_filename": "SpawnData.csv",
  "skipped_entries_filename": "SkippedEntries.csv",
  "MAX_WORKERS": 8,
  "LOG_FILENAME": "process_log.txt",
  "LOG_LEVEL": "INFO",
  "FUN_MODE": true
}
```

## Usage
To run the Cobblemon Spawn Data Extractor:
```bash
python cobblemon_spawndata_processor.py
```

The script will process the archives, extract relevant JSON files, and generate a CSV file with the extracted data. If `FUN_MODE` is enabled, you will see colorful messages during the processing.

## Docker Setup
A Docker container can be used to make running this project easier and consistent across environments.
1. **Create a Dockerfile** in the project root:
    ```dockerfile
    FROM python:3.10-slim
    WORKDIR /app
    COPY . /app
    RUN pip install -r requirements.txt
    CMD ["python", "cobblemon_spawndata_processor.py"]
    ```
2. **Build the Docker Image**:
    ```bash
    docker build -t cobblemon-extractor .
    ```
3. **Run the Docker Container**:
    ```bash
    docker run --rm -v $(pwd):/app cobblemon-extractor
    ```

## Fun Mode
`Fun Mode` adds colorful messages to the output to make the process more engaging.
- To enable fun mode, set `"FUN_MODE": true` in `config.json`.
- The script uses `colorama` to color code messages, making it easier to track progress and spot errors.

## Logging
Logs are generated to track the progress and status of processing. The logs are saved to `process_log.txt` by default (configurable via `LOG_FILENAME`).

## Contributing
Contributions are welcome! Feel free to fork the repository and submit a pull request.

## License
This project is licensed under the MIT License. See `LICENSE` for more information.

## Google Sheet Example
The output CSV generated by this script can be viewed in a sample Google Sheet:
[Spawn Data Spreadsheet for BCG Plus (w Cobblemon)](https://docs.google.com/spreadsheets/d/1bphOi2A7DawLSWsk92Y-welkX48UrBKOfE141xIZgdw/edit?usp=sharing)

## Acknowledgements
Special thanks to the Cobblemon team and all contributors for making this project possible!

