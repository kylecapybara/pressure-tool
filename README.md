# Equilibrium Pressure Extractor

An interactive web-based tool for easily analyzing VLE (Vapor-Liquid Equilibrium) lab pressure data from lab experiments (specifically designed for CHEG345 at UD). I was looking around for a simple tool with all the functionality I needed to quickly analyze pressure signals and couldn't find it. So I made it! 

<img src="screenshot.png" alt="screenshot of the program" width="600"/>

[CLICK HERE TO USE THE TOOL](https://kylecapybara.github.io/pressure-tool/equilibrium_pressures.html)


## Features

- **Load CSV Files**: Upload custom data files with any columns
- **Column Selection**: Choose which columns to use for X and Y axes with dropdowns (defaults to column 1 for X, column 2 for Y)
- **Interactive Chart**: Visualize data with Chart.js
- **Region Selection**: Drag on the chart to define analysis regions
- **Region Editing**: 
  - Drag region edges to resize
  - Drag region middle to move
  - Remove individual regions
- **Statistical Analysis**: Automatically calculates mean, standard deviation, and point count for each region
- **Export Results**: 
  - Export region statistics as a CSV file with save dialog
  - Copy results directly to clipboard

## Usage

1. Open `equilibrium_pressures.html` in a web browser
2. Click **Load custom CSV** to select your data file
3. The tool expects CSV format with at least 2 columns (any numeric data)
4. Select **X axis** and **Y axis** columns from dropdowns (defaults to columns 1 & 2)
5. Drag on the chart to create regions
6. Resize or move regions as needed
7. Export results:
   - Click **Export CSV** to download as file with save dialog
   - Click **Copy to Clipboard** to copy CSV data directly

## Column Support

The tool automatically detects and lists all CSV columns. You can:
- Use any columns for X and Y axes
- Work with various time formats: numeric values, ISO datetime strings, or HH:MM:SS.microseconds
- Toggle between columns without reloading the file

## Export Format

The exported CSV contains:
- `region`: Region number (sorted by x_start)
- `x_start`: Start time of region
- `x_end`: End time of region
- `mean_signal`: Mean signal value in region
- `std_signal`: Standard deviation of signal in region
- `n_points`: Number of data points in region

All values are formatted to 8 significant figures.

## Technologies

- [Chart.js 4.3.0](https://www.chartjs.org/) - Chart visualization
- [PapaParse 5.3.2](https://www.papaparse.com/) - CSV parsing
- Modern browser with File System Access API support (fallback to standard download)

## Notes

- Values are automatically normalized relative to the first data point (on X axis)
- Hover over regions to see edit options (resize edges or move)
- Clear all regions with the **Clear all regions** button
- Column selectors are available after loading a CSV file
- Change column selections to re-plot the chart instantly without reloading
