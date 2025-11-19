# weather-data
From 2014 to 2025 I've run a hobby weather station at my home in Loughrea, Ireland.  This is its data.

Sadly, in November 2025, the receiving console has reached the end of its memory.  Although it is still receiving data from external sensors, it has lost the capacity to save them to memory, or make them available for live processing. I've decided to make the historical logs available to all, in the hope they provide some utility.

If you do make use of this data, I'd be delighted to hear of your use case.

## The Setup
The weather station is a N96GY home/hobby weather station.

This I configuired to take a reading every 5 minutes, and process that data with [PyWWS v22.10.0](https://pywws.readthedocs.io/en/latest/) running on a [Raspberry Pi](https://www.raspberrypi.com/)

## The Data
Data is organised in folders labled by year and month.  Within the month folder, each day is represented as a CSV file.

All times are recorded in **UTC** (Coordinated Universal Time). The typical units are meters per second (m/s) for wind, degrees Celsius (°C) for temperature, hectopascals (hPa) for pressure, and millimeters (mm) for rainfall.

| # | Field Value | Field Name | Unit | Description |
| :---: | :--- | :--- | :--- | :--- |
| **1** | `2014-03-27 23:09:48` | **Date & Time (idx)** | UTC | The **UTC timestamp** for the weather log record. |
| **2** | `5` | **Interval/Delay** | Minutes | The logging interval used by the station in minutes (5 minutes). |
| **3** | `59` | **Indoor Humidity** | % | Indoor Relative Humidity. |
| **4** | `17.7` | **Indoor Temperature** | °C | Indoor Temperature. |
| **5** | `79` | **Outdoor Humidity** | % | Outdoor Relative Humidity. |
| **6** | `1.0` to `1.4` | **Outdoor Temperature** | °C | Outdoor Temperature. |
| **7** | `1010.2` | **Absolute Pressure** | hPa | The **absolute** (station) barometric pressure reading. |
| **8** | `1015.1` | **Relative Pressure** | hPa | The **relative** (sea-level equivalent) barometric pressure, calculated from the absolute pressure. |
| **9** | `1.4` | **Average Wind Speed** | m/s | Average wind speed since the previous log interval. |
| **10** | `1.7` | **Wind Gust** | m/s | Maximum wind gust speed recorded since the previous log interval. |
| **11** | `2` | **Rainfall** | 0.3mm units | Accumulated rainfall **since the last log record**. This value is often stored in units of 0.3 mm on the console. |
| **12** | `280.2` | **Wind Direction** | Degrees | Wind direction in degrees (0 = North, 90 = East, 180 = South, 270 = West). |
| **13** | `0` | **Status** | Integer | Status code (e.g., used to indicate a sensor error, battery low, or rain counter overflow). `0` means no error. |

## Notes
**Rainfall Units**: The rainfall field (Field 11) is typically recorded as the count of tipping bucket events. For many weather stations, each "tip" represents ~0.3 mm of rain. To get the actual rainfall in millimeters for the period, you would multiply this count by 0.3. The values can jump, for example 2 to 0 to 14 to 10, indicating sporadic rain showers occurred during the period.

Further information on file format can be found in the PyWWS documentation.