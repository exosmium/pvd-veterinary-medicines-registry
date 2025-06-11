# PVD Veterinary Medicines Registry

This repository automatically downloads and processes veterinary medicines data from the Latvian Food and Veterinary Service (PVD) registry.

## Data Source

The data is sourced from: https://registri.pvd.gov.lv/open-data/download?register=vz&type=json&ver=1/

## Automated Updates

The repository is updated daily at 2 AM UTC via GitHub Actions. The workflow:

1. Downloads the latest ZIP file from the PVD registry
2. Extracts the `vz-dati.json` file
3. Processes the data to extract only medicine names
4. Creates a simplified JSON file with the format: `[{"name": "Medicine Name"}, ...]`
5. Commits the updated data back to the repository

## Accessing the Data

### Processed Medicine Names
- **File**: [`data/medicines.json`](data/medicines.json)
- **Format**: Array of objects with `name` field
- **Example**:
```json
[
  {"name": "Clavubactin 50/12,5 mg tablet"},
  {"name": "Clavubactin 250/62,5 mg tablet"},
  ...
]
```

### Summary Information
- **File**: [`data/summary.json`](data/summary.json)
- **Contains**: Last update timestamp, total count, and metadata

## Raw Data Access

You can access the processed data directly via GitHub's raw content URLs:

- **Medicines**: `https://raw.githubusercontent.com/exosmium/pvd-veterinary-medicines-registry/main/data/medicines.json`
- **Summary**: `https://raw.githubusercontent.com/exosmium/pvd-veterinary-medicines-registry/main/data/summary.json`

## Manual Trigger

You can manually trigger the data update by going to the [Actions tab](../../actions) and running the "Update Veterinary Medicines Registry" workflow.

## Data Fields in Original Source

The original data contains these fields (we only extract `OriginalaisNosaukums`):
- `ZaluID`: Medicine ID
- `OriginalaisNosaukums`: Original medicine name (extracted)
- `StarptautiskaisNosaukums`: International name
- `RegistracijasApliecibasIpasnieks`: Registration certificate owner
- `Razotaji`: Manufacturers
- `RegistracijasNumurs`: Registration number
- `ATKKods`: ATC code
- `RegistracijasProcedura`: Registration procedure
- `RegistracijasDatums`: Registration date
- `RegistracijasBeigas`: Registration end date
- `IzsniegsanasKartiba`: Dispensing order
- `Stiprums`: Strength
- `ZaluFormaLV`: Medicine form (Latvian)
- `ZaluFormaEN`: Medicine form (English)
- `SugasLV`: Species (Latvian)
- `SugasEN`: Species (English)

## License

This project processes public data from the Latvian Food and Veterinary Service. The original data is provided under their terms of use. 