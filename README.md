Here's a README that highlights the use of Airflow for ETL and the integration of D3.js, JavaScript, and Python for visualization:

# Project: ETL and Data Visualization with Airflow, D3.js, JavaScript, and Python

## Overview

This project demonstrates an ETL (Extract, Transform, Load) process using Apache Airflow and showcases data visualization using D3.js. The goal is to extract course catalog data from MIT's website, transform the data to clean and analyze it, and visualize the results in a dynamic bubble chart.

## Prerequisites

- Docker and Docker Compose
- Python 3.x
- Apache Airflow
- Node.js and npm (for local development of D3.js visualizations)

## Setup

### Step 1: Set up the Airflow Environment

1. **Clone the repository**:
   ```sh
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Start Airflow using Docker Compose**:
   ```sh
   docker-compose up -d
   ```

3. **Access the Airflow web interface**:
   Open your browser and go to `http://localhost:8080`.

### Step 2: Configure Airflow DAG

1. **Upload DAG and supporting files**:
   - Copy `assignment.py` to the Airflow DAGs directory.
   - Copy `00_urls.txt` to the Airflow DAGs directory.

   ```sh
   docker cp assignment.py airflow-docker_airflow-scheduler_1:/opt/airflow/dags/
   docker cp 00_urls.txt airflow-docker_airflow-scheduler_1:/opt/airflow/dags/
   ```

2. **Start the DAG**:
   - In the Airflow web interface, enable and trigger the `assignment` DAG.

### Step 3: Data Visualization with D3.js

1. **Place the visualization files**:
   - Copy `d3_bubble_chart_example.html` and `words.js` to your local web server directory or serve them using a simple HTTP server.

   ```sh
   python -m http.server 8000
   ```

2. **Access the visualization**:
   Open your browser and go to `http://localhost:8000/d3_bubble_chart_example.html`.

## Project Structure

- `assignment.py`: The main Airflow DAG script that defines the ETL pipeline.
- `00_urls.txt`: A text file containing URLs of MIT course catalogs.
- `d3_bubble_chart_example.html`: The HTML file for the D3.js bubble chart visualization.
- `words.js`: The JSON file containing word frequency data for the visualization.

## Airflow DAG Explanation

The Airflow DAG (`assignment.py`) consists of the following tasks:

1. **Task 0 - Install BeautifulSoup**:
   - Installs the BeautifulSoup library using a Bash command.

2. **Task 1 - Catalog**:
   - Extracts HTML content from the URLs listed in `00_urls.txt` and saves them to individual files.

3. **Task 2 - Combine**:
   - Combines all the HTML files into a single file `combo.txt`.

4. **Task 3 - Titles**:
   - Extracts the course titles from the combined HTML file and saves them in `titles.json`.

5. **Task 4 - Clean**:
   - Cleans the titles by removing punctuation, numbers, and one-character words, then saves the cleaned titles in `titles_clean.json`.

6. **Task 5 - Count Words**:
   - Counts the frequency of each word in the cleaned titles and saves the counts in `words.json`.

## D3.js Visualization Explanation

The D3.js visualization (`d3_bubble_chart_example.html`) displays a dynamic bubble chart representing the frequency of words extracted from the course titles.

- **Dataset Preparation**:
  - The `words.js` file is included, which contains the word frequency data.
  - Filters out common stopwords (e.g., "and", "in", "to", "for", "of", "the") from the visualization.

- **Bubble Chart Configuration**:
  - Sets the dimensions for the SVG element.
  - Creates a D3 pack layout to arrange the bubbles.
  - Appends circles and text elements to represent the words and their frequencies.
  - Adds animation to the bubbles to make them move dynamically.

## Conclusion

This project demonstrates the power of combining Airflow for ETL processes with D3.js for interactive data visualization. By leveraging Python for data extraction and cleaning, and JavaScript for front-end visualization, we can create insightful and engaging data representations.
