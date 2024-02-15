# Project Math: Demography Analyzer

## Overview

The Demography Analyzer is a Python application designed to analyze and predict population growth trends. Utilizing demographic data, it calculates linear fits to estimate population growth and correlates these estimates with actual data to provide insights into future population numbers.

## Features

- Load demographic data from CSV files.
- Calculate linear fits for population data (Fit 1 and Fit 2 methods).
- Estimate future population numbers for the year 2050.
- Compare population growth among different countries.
- Calculate root-mean-square deviation to evaluate fit accuracy.
- Correlation calculation between population data and years.

## Requirements

- Python 3.x
- CSV file with demographic data (provided as `105demography_data.csv` by default)

## Usage

To use the Demography Analyzer, execute the script from the command line with country codes as arguments:

```
./main.py [country_code]+
```

Example:

```
./main.py US JP
```

This command analyzes and compares the demographic trends of the United States and Japan.

## Help

For usage instructions, run:

```
./main.py -h
```

## Contributing

Contributions to the Demography Analyzer are welcome. Please ensure to follow coding standards and include tests with your pull requests.
