# Web Scraping and Data Storage Project

This project is a Python-based web scraping application that extracts upcoming event information from a specified webpage, stores the data in an SQLite database, and sends an email notification if new events are detected. The project uses the `requests`, `selectorlib`, and `sqlite3` libraries to scrape, parse, and store the data.

## Table of Contents
- [Overview](#overview)
- [Requirements](#requirements)
- [Project Structure](#project-structure)
- [Setup](#setup)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Additional Information](#additional-information)

## Overview
The script scrapes event information such as location, city, and date from a given URL, and checks if the event is already present in an SQLite database (`data.db`). If the event is new, it is added to the database, and a placeholder email notification is sent.

## Requirements
- Python 3.x
- Required Python libraries:
  - `requests`
  - `selectorlib`
  - `sqlite3` (included in Python standard library)

Install the required libraries using:
```bash
pip install requests selectorlib
```

## Project Structure

├── extract.yaml     # YAML file defining the structure of elements to be extracted from the webpage

├── main.py          # The main script for scraping, extracting, storing data, and sending notifications

├── data.db          # SQLite database file storing event information

├── README.md        # This README file

## Setup
1. Clone or download this repository to your local machine.
2. Create an SQLite database file named data.db and a table called events using the following SQL query:
```bash
CREATE TABLE events (
    location TEXT,
    city TEXT,
    date TEXT
);
```
3. Create an `extract.yaml` file in the same directory with the following content:
```bash
tours:
    css: 'div.tour'
    multiple: true
    type: Text
```
The CSS selector `div.tour` should match the elements in the webpage containing event information. Adjust the selector as needed for your target webpage structure.

## Usage
1. Run the script using:
```bash
python main.py
```
2. The script will:
- Scrape the target URL defined in the `URL` variable.
- Extract event information (location, city, and date).
- Check if the events are already stored in the `data.db` SQLite database.
- If new events are found, they will be added to the database, and a placeholder email notification will be sent.

## How It Works
1. Scraping:
- The `Event` class contains the `scrape` function, which sends an HTTP request to the given URL and retrieves the HTML content.
2. Extraction:
- The `extract` function in the `Event` class uses `selectorlib` to parse and extract data based on the `extract.yaml` configuration.
3. Database Storage:
- The `Database` class connects to an SQLite database, and the `store` function inserts extracted data into the `events` table.
4. Checking for Duplicates:
- The `read` function queries the database to check if an event is already stored to avoid duplicate entries.
5. Sending Email:
- The `send` function in the `Email` class is a placeholder that currently only prints "Email sent". It can be modified to send real email notifications using `smtplib` or another service.

## Additional Information
- Modify the CSS selector in extract.yaml as needed to match the target webpage's structure.
- Expand the project by implementing an actual email-sending functionality in the Email class.
- Adjust the database schema or YAML file configuration to extract and store different types of data.
If you encounter any issues or have suggestions for improving this project, feel free to open an issue or submit a pull request.
```bash

### Key Notes:
- Ensure that the CSS selector defined in `extract.yaml` correctly targets the elements you want to extract from the webpage.
- The `Email` class currently only contains a placeholder function for sending an email. You can implement this functionality using libraries like `smtplib` or third-party services like SendGrid or Mailgun.
- The SQLite database schema should match the structure of the extracted data to ensure correct data storage.

If you need help with any part of this implementation or wish to add more features, let me know!
```
