# Python Web Scraper

Production-quality Python web scraper that extracts structured product data from a public website, cleans and deduplicates it, and exports the results to Excel and CSV.

![Project thumbnail](./thumbnail.svg)

## Overview

This project scrapes product listings from [Books to Scrape](https://books.toscrape.com/), a public demo website designed for scraping practice. It collects product records across multiple pages, normalizes the data, and saves the final output as a clean Excel workbook.

The project is built to be reusable, portfolio-ready, and easy to customize for other public listing sites.

## Features

- Multi-page scraping with configurable page count
- Structured extraction with `requests` and `BeautifulSoup`
- Data cleaning and deduplication with `pandas`
- Excel export with basic formatting via `openpyxl`
- Optional CSV export
- Retry handling for temporary request failures
- Graceful handling of missing HTML elements
- CLI arguments for easy reuse

## Tech Stack

- Python 3
- requests
- BeautifulSoup4
- pandas
- openpyxl

## Target Website

- Site: `https://books.toscrape.com/`
- Data type: Product listings
- Access: Publicly accessible, no login required

## Fields Extracted

- `product_name`
- `price_gbp`
- `rating`
- `availability`
- `product_url`

## Project Structure

- `scraper.py` - main scraping script
- `requirements.txt` - Python dependencies
- `README.md` - project documentation
- `sample_output.xlsx` - sample Excel export

## Quick Start

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

Run the scraper:

```powershell
python scraper.py
```

## CLI Usage

Default run:

```powershell
python scraper.py
```

Scrape 5 pages:

```powershell
python scraper.py --pages 5
```

Export both Excel and CSV:

```powershell
python scraper.py --pages 5 --csv
```

Write to a custom output file:

```powershell
python scraper.py --output my_products.xlsx
```

Use a different paginated URL template:

```powershell
python scraper.py --base-url "https://example.com/catalog/page/{}"
```

## Example Result

The default run creates:

- `scraped_data.xlsx`
- `scraped_data.csv` when `--csv` is used

The included [sample_output.xlsx](C:/Users/rahul/Documents/Codex/2026-04-21-build-a-production-quality-python-web/sample_output.xlsx) shows the final Excel structure and formatting.

## How It Works

The scraper follows a simple modular flow:

1. `fetch_page(url)` retrieves HTML with retries and timeout handling.
2. `parse_data(html)` extracts product records from each listing page.
3. `clean_data(dataframe)` normalizes values, removes duplicates, and fixes types.
4. `save_to_excel(dataframe)` writes the final cleaned dataset to Excel.

## Customization

To adapt this project for another public site:

1. Update `DEFAULT_BASE_URL` in `scraper.py`
2. Change the CSS selectors in `parse_data()`
3. Adjust cleaning logic in `clean_data()`
4. Update `OUTPUT_COLUMNS` to match the new schema

## Error Handling

- Uses a retry-enabled `requests.Session`
- Handles timeouts and request failures without crashing the run
- Skips failed pages after retries are exhausted
- Safely handles missing or incomplete HTML elements
- Adds a delay between requests to avoid overloading the target site

## Portfolio Value

This project demonstrates practical scraping workflow design, modular Python scripting, data cleaning, and file export automation. It is a strong starter template for e-commerce, directory, or listing-based scraping projects.
