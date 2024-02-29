# Africa Gas Tracker

Project with [GEM](globalenergymonitor.org), based largely on [Asia Gas Tracker](https://greeninfo-network.github.io/asia-gas-tracker), with different types categories, and improvements adopted from [GOIT](https://greeninfo-network.github.io/global-oil-infrastructure-tracker/)

## Hosting

On GEM via iFrame, served from GH pages
https://greeninfo-network.github.io/africa-gas-tracker


## Development

Pre-requisites: 
* Node and npm
* Yarn

To match the development node version:
```
nvm use
```

First time only:
```
npm install
```

To start a development server:
```
npm run start
```


## Production
```
npm run build
```

The app is hosted on GitHub pages (via the `docs/` folder).

## Data Management

There are several data sources
* Country boundaries (see the `documentation/update_country_geojson` directory for details)
* A single Google spreadhsheet is used to manage pipeline and terminal data. Currently these are combined directly in Sheets for export from a single tab named `data_export`
https://docs.google.com/spreadsheets/d/1mwH60IUtgcejv9_bEhIRD7pKft2Qtc7p1p49E5H9y1M/edit#gid=1855199080

Update: Mason is now sending CSV data directly. This bypasses the need for us to export from the Google Sheet, above. But the types and statuses still need to match our expectations. 


## Data formatting

* Terminals are simply parsed from `lat` and `lng` columns in the csv data sheet.
* Pipelines, however, use a custom-delimeneted format for lines in the `route` column. Segments are delimited with semi-colons, and coordinate pairs are separated by colons. The coordinates themselves are separated by a comma:   
```
-33.5020763,147.7848194:-33.385745,148.006048:-33.136884,148.171628:-32.2378573,148.2389384:-32.2241903,148.6155634:-32.548010, 148.936829
```

## Data update

1. GEM will send us a raw data spreadsheet. After checking that column order hasn't changed, drop this in the `raw_data` tab on [this spreadsheet](https://docs.google.com/spreadsheets/d/1mwH60IUtgcejv9_bEhIRD7pKft2Qtc7p1p49E5H9y1M/edit#gid=1855199080) and then export the `data_export` tab to `data/data.csv`
2. Then see `documentation/update_country_geojson/readme.md` for details on matching up country names in the data to country names in `world.json` to produce `data/countries.json`

## Testing new data

1. After every data update, there are often pipelines that won't correctly parse. Check the console for any error messages, then email the client the names of any pipelines that need work. 
