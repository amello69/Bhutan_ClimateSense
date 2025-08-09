# GraphCast GFS Data Downloader

This Colab notebook provides a simple Python script to download experimental GraphCast Global Forecast System (GFS) data from NOAA's public S3 bucket. The data includes medium-range global forecasts at a 0.25-degree resolution.

---

## 🚀 How It Works

The notebook automates the download of GRIB2-formatted forecast files for specified dates and forecast cycles. It leverages the `requests` library to fetch data directly via HTTP and saves it to your Google Drive for easy access and persistence.

---

## ✨ Features

* **Automated Downloads:** Easily download multiple forecast hours for a given date and cycle.

* **Google Drive Integration:** Saves downloaded files directly to your Google Drive, preventing data loss when your Colab session ends.

* **Organized Output:** Files are automatically stored in a date-named subdirectory within your specified download folder, keeping your data tidy.

---

## 🛠️ Setup and Usage

Follow these steps to use the notebook in Google Colab:

1.  **Open in Google Colab:** Upload this notebook to your Google Drive and open it with Google Colab.

2.  **Mount Google Drive:** Run the first code cell that contains:

    ```python
    from google.colab import drive
    drive.mount('/content/gdrive')
    ```

    This will prompt you to authenticate and grant Colab access to your Google Drive. Follow the on-screen instructions.

3.  **Define `download_graphcast_gfs` function:** Run the cell containing the `download_graphcast_gfs` function definition. This function handles the logic for constructing the correct S3 URL and downloading the GRIB2 files.

4.  **Execute the Main Loop:** Run the cell with the main download loop. You can modify the `date`, `cycle`, and `forecast_hours` lists to customize your downloads.

    * `date`: The forecast date in `YYYYMMDD` format (e.g., `'20250730'`).

    * `cycle`: The forecast cycle in `HH` format (e.g., `'00'`, `'06'`, `'12'`, `'18'`).

    * `forecast_hour`: The forecast lead time in `HHH` format (e.g., `'000'` for analysis, `'006'` for 6-hour forecast).

5.  **Access Downloaded Data:** Your downloaded files will be located in your Google Drive under `My Drive/graphcastgfs_downloads/YYYYMMDD/`, where `YYYYMMDD` is the date you specified.

---

## 📂 Data Structure

The GraphCast GFS data in the S3 bucket and, consequently, your downloaded files are organized as follows:

* **Base URL:** `https://noaa-nws-graphcastgfs-pds.s3.amazonaws.com/`

* **Date-stamped folders:** `graphcastgfs.YYYYMMDD/` (e.g., `graphcastgfs.20250730/`)

* **Individual Forecast Files:** Inside each date folder, files follow the pattern:
    `graphcastgfs.tCCh.pgrb2.0p25.fHHH`

    * `CC`: Forecast cycle (00, 06, 12, or 18 UTC)

    * `HHH`: Forecast hour (e.g., 000, 006, 012, ..., 072)

**Example File Path:**
`/content/gdrive/MyDrive/graphcastgfs_downloads/20250730/graphcastgfs.t00z.pgrb2.0p25.f000`

---

## ⚠️ Important Notes

* This system is experimental, and data availability may vary.

* The data is in GRIB2 format, which requires specialized libraries (e.g., `cfgrib`, `xarray` with `eccodes`) for processing in Python. You might need to install these in your Colab environment if you plan to analyze the data.

* Ensure sufficient space on your Google Drive for downloads, as GRIB2 files can be large.
