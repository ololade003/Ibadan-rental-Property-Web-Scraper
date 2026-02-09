# Ibadan Rental Property Web Scraper (PrivateProperty.ng)

## Project Overview
This project is a Python web scraping pipeline designed to collect, clean, and structure rental apartment listings in Ibadan, Oyo State, Nigeria from PrivateProperty.ng.
The scraper extracts non-sponsored (organic) listings only, enriches the raw data with parsed dates, inferred property features, and standardized locations, then exports the final dataset to a CSV file ready for analysis or visualization.
This project was built as part of a broader real estate market pricing and affordability analysis

## Objectives
-Scrape Ibadan apartment rental listings from PrivateProperty.ng

-Exclude sponsored listings to avoid price bias

-Extract and clean:

  * Price
  
  * Location
  
  * Bedrooms, bathrooms, toilets
  
  * Listing date (standardized)
  
  * Property type
  
-Map unstructured addresses to known Ibadan areas

-Export a clean, analysis-ready dataset

## Tools and Libraries used

* ### Python

* requests – HTTP requests

* BeautifulSoup – HTML parsing

* pandas & numpy – data cleaning and structuring

* re – pattern matching

* datetime – date normalization

* time & random – polite scraping delays


## Data Source
* Website: PrivateProperty.ng

* Category: Flats & Apartments for Rent

* Search Scope: Ibadan, Oyo State

* Pagination: Pages 0 – 15

##### ⚠️This scraper is intended for educational and research purposes only.
##### Always review a website’s robots.txt and terms of service before scraping.

## Key Features & Implementation Details

### 1️⃣ Page Navigation & Polite Scraping:

* Iterates through multiple result pages using query parameters

* Adds randomized delays (3–6 seconds) between requests to reduce server load

* Uses custom request headers to mimic a real browser

### 2️⃣ Sponsored Listings Filtering

* PrivateProperty.ng mixes sponsored and organic listings.

* This scraper explicitly filters out sponsored listings by excluding elements with the class: 'sponsored-listing'

* Only natural listings are collected to ensure unbiased pricing analysis.

### 3️⃣ Robust Listing Date Parsing

##### Listing dates appear in inconsistent formats such as:

* Added Today

* Updated Yesterday

* Added 12 Jan 2024

* Updated 03 Dec 2023

##### A custom date parser:

* Handles relative dates

* Extracts absolute dates using regex

* Prioritizes Added dates over Updated where both exist

* Converts all dates to standard YYYY-MM-DD format

### 4️⃣ Property Features Extraction

Bedrooms, bathrooms, and toilets are extracted from the listing’s feature icons.

The scraper:

* Handles missing or incomplete feature data gracefully

* Ensures numeric consistency

* Casts values to nullable integer types (Int64)

### 5️⃣ Location Normalization (Ibadan Areas)

Listing addresses are unstructured text strings.

To standardize locations:

* An external Excel file of known Ibadan areas is loaded

* Each listing address is scanned using word-boundary regex matching

* The first matching area is extracted into a new Location column

This improves grouping, filtering, and spatial analysis.

### 6️⃣ Property Type Inference

Property types are inferred directly from listing titles using keyword matching:

* Block of Flats

* Mini Flat

* Self Contain

* Shared Apartment

This creates a structured property_type field for analysis.


## 🚀 How to Run the Project

#### 1. Clone the repository

* git clone https://github.com/ololade003/Ibadan-rental-Property-Web-Scraper.git


#### 2. Install dependencies

* pip install requests beautifulsoup4 pandas numpy openpyxl


#### 3. Update the path to the Ibadan areas reference file:

* streets_df = pd.read_excel("path/to/ibadan_areas_reference_only.xlsx")


#### 4. Run the notebook or script

#### 5. Output file:

* Ibadan_city_homes_for_rent.csv

## 🔮 Possible Enhancements

* Add fuzzy matching for misspelled locations

* Include latitude & longitude (geocoding)

* Extend scraping to other Nigerian cities

* Automate daily or weekly data collection

* Add price trend and affordability analysis
