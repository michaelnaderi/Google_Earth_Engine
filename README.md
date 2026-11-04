# Google Earth Engine scripts and notebooks

This is where I keep the Earth Engine work I do on water, climate and land: rainfall, drought, snowmelt, lakes, floods, vegetation and land cover. Most of it started as quick scripts in the Earth Engine Code Editor while I was exploring a dataset or answering a question for a project. Over time I've been turning the more useful ones into Python notebooks that run from start to finish, save their figures and tables, and are easier for other people to pick up.

Everything here is free to use. If something helps your research, teaching or a side project, go ahead, and I'd love to hear about it.

![Example results](figures/linkedin_showcase.png)

## What's in here

The repository has two kinds of files.

### Jupyter notebooks (Python)

These are the more complete versions. Each one pulls data from Earth Engine, runs the analysis, and saves figures to `figures/` and tables to `outputs/`.

| Notebook | What it does |
|---|---|
| `modis_cropland_analysis.ipynb` | Yearly cropland area in western Kansas from MODIS land cover (2001 onwards), trends and maps of where cropland was gained or lost |
| `Landsat_Vegetation_Indices_Virginia.ipynb` | 8-day NDVI, EVI and LAI composites from Landsat 8/9 for all of Virginia, broken down by land cover |
| `spei_drought_analysis.ipynb` | Drought monitoring with the 12-month SPEI: drought classes, drought events and trends |
| `Standardized_Precipitation_Index(SPI)_PERSIANN.ipynb` | Standardized Precipitation Index from PERSIANN-CDR rainfall |
| `Precipitation_Intensity_Index.ipynb` | Rainfall intensity (SDII) and extremes such as wet days, heavy rain days and the wettest day of the year |
| `GPM_Precipitation_Aggregation.ipynb` | Half-hourly GPM IMERG rainfall summed to daily, monthly and annual totals, with maps and GeoTIFF export |
| `SARIMAX_Precipitation_Forecast.ipynb` | Monthly rainfall forecast with a seasonal ARIMA model, checked against a simple climatology baseline |
| `ERA5_Snowmelt_Temperature.ipynb` | Spring temperature and snowmelt timing in a river basin from ERA5-Land |
| `ML_on_GRACE_data.ipynb` | Machine learning on GRACE groundwater/terrestrial water storage data |

### Earth Engine Code Editor scripts (JavaScript)

The files without an extension (for example `Cropland_Area`, `Snow_Cover`, `Water_Bodies_Area`) are the original Code Editor scripts. Copy one into [code.earthengine.google.com](https://code.earthengine.google.com), draw or import your own `geometry`, and press Run. They cover a wider range of topics than the notebooks so far, including snow cover, evapotranspiration, chlorophyll in water bodies, urban flood detection with Sentinel-1, vegetation health, and machine learning to sharpen coarse datasets (ERA5 temperature, GRACE, land cover).

## Running the notebooks

You'll need a Google Earth Engine account linked to a Google Cloud project (free for non-commercial and research use; you can register at [code.earthengine.google.com/register](https://code.earthengine.google.com/register)).

1. Install the packages:
   ```
   pip install earthengine-api numpy pandas matplotlib scipy statsmodels requests pillow
   ```
2. Sign in once from Python. This opens a browser window:
   ```python
   import ee
   ee.Authenticate()
   ```
3. In the setup cell of the notebook, replace `"add your GEE username"` with your own project ID.
4. Run all cells from the top (**Kernel → Restart & Run All**).

To use your own study area, change the region in the parameters cell near the top. The defaults are places I was working on at the time (western Kansas, Virginia and so on), but the notebooks aren't tied to them.

A few practical notes:

- Some notebooks do a lot of work in Earth Engine (whole states, many years, daily data). They save results to `outputs/` as they go, so if the kernel restarts or a request times out, running them again picks up where they stopped instead of starting over.
- If you change the study area or dates, set `FORCE_RECOMPUTE = True` once, or use new output folder names, so old results aren't reused.
- Satellite products have limits: coarse pixels, clouds, snow, terrain. I've tried to note the main ones at the end of each notebook. Please read those before using the numbers for anything important.

## Contributing

Contributions are very welcome. That could be a fix, a new dataset or method, a version of a script for another region, or just an issue telling me something doesn't work. Have a look at [CONTRIBUTING_TO_GEE_CODES.md](CONTRIBUTING_TO_GEE_CODES.md), then open an issue or send a pull request.

## License

See the [LICENSE](LICENSE) file.

## Contact

Mehdi Naderi — feel free to reach out through GitHub issues, or connect with me on LinkedIn.
