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
- **Statistical Analysis**: Automatically calculates mean, standard deviation, and point count for each region; updates in real-time during correction adjustments
- **Linear Drift Correction**:
  - Enable/disable with checkbox
  - Adjust slope with high-precision slider (0 to 0.005, step 0.00001)
  - Type slope value directly for precise input
  - Customize slider range with min/max inputs
  - Drag vertical bar on chart to set correction start position
  - Auto-calculated intercept maintains original signal value at start point
- **X-axis Zoom**: Hold Shift and drag to zoom; use "Reset X Zoom" button to restore
- **Significant Figures Control**: Select 3–8 significant figures for export
- **Export Results**: 
  - Export region statistics as a CSV file with save dialog
  - Copy results directly to clipboard (paste-able into Excel/Google Sheets!)
  - Exports corrected values if correction is active

## Usage

### Basic Workflow

1. Open `equilibrium_pressures.html` in a web browser
2. Click **Load custom CSV** to select your data file
3. The tool expects CSV format with at least 2 columns (any numeric data)
4. Select **X axis** and **Y axis** columns from dropdowns (defaults to columns 1 & 2)
5. Define regions:
   - Drag on the chart to create a region
   - Resize by dragging region edges
   - Move by dragging region center
   - Remove with the red button in the table
6. (Optional) Apply linear drift correction:
   - Check **Linear correction** to enable
   - Drag the orange vertical bar to set where correction starts
   - Adjust **Slope (m)** with slider or by typing directly
   - Customize slider range with **Range** min/max inputs
   - Statistics update in real-time
7. Export results:
   - Click **Export CSV** to download with save dialog
   - Click **Copy to Clipboard** to paste into spreadsheets
   - Adjust significant figures (3–8) before exporting

### Linear Drift Correction

Linear drift correction removes a linear trend from signal data:

$$y_{\text{corrected}}(x) = y(x) - m(x - x_{\text{start}})$$

Where:
- **m** (Slope): Drift rate per unit time (range: 0 to 0.005, user-customizable)
- **x_start**: Time point where correction begins (orange draggable bar on chart)
- The signal value **remains unchanged at x_start**, preventing discontinuities

**Example**: If pressure drifts down at 0.001 mbar/min, set slope = 0.001 to remove this trend before equilibrium calculations.

## Column Support

The tool automatically detects and lists all CSV columns. You can:
- Use any columns for X and Y axes
- Work with various time formats: numeric values, ISO datetime strings, or HH:MM:SS.microseconds
- Toggle between columns without reloading the file

## Documentation

For detailed *technical* documentation including the mathematical model, architecture, and implementation details, see **[DOCUMENTATION](https://kylecapybara.github.io/pressure-tool/DOCUMENTATION.html)** webpage. or [DOCUMENTATION.qmd](DOCUMENTATION.qmd) or or [DOCUMENTATION.pdf](DOCUMENTATION.pdf).

Topics covered:
- Data loading and normalization
- Linear drift correction mathematics and derivation
- Region statistics computation
- Chart visualization with custom plugins
- Export formats and numerical considerations
- Browser compatibility and performance notes


## Export Format

The exported CSV contains:
- `region`: Region number (sorted by x_start)
- `x_start`: Start index of region in data
- `x_end`: End index of region in data
- `mean_signal`: Mean signal value in region (corrected if correction enabled)
- `std_signal`: Standard deviation of signal in region
- `n_points`: Number of data points in region

All values are formatted to your selected significant figures (default: 6). Choose from 3–8 figures before exporting.

## Technologies

- [Chart.js 4.3.0](https://www.chartjs.org/) - Chart visualization
- [PapaParse 5.3.2](https://www.papaparse.com/) - CSV parsing
- Modern browser with File System Access API support (fallback to standard download)

## Notes

- Values are automatically normalized relative to the first data point (on X axis)
- Hover over regions to see edit options (resize edges or move)
- Clear all regions with the **Clear all regions** button
- Linear correction start point (orange bar) can be dragged interactively
- Statistics automatically recalculate when correction is adjusted or toggled
- Use **Reset correction** button to disable correction and restore original values
- Column selectors are available after loading a CSV file
- Change column selections to re-plot the chart instantly without reloading
