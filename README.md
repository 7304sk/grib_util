# grib_util

Read and download grib files from various weather agencies (ex: JMA, ECMWF, etc.)

## install

```Bash
pip install git+https://github.com/7304sk/grib_util.git
```

## Usage

### ERA5

```python
from grib_util import ERA
# Download (Files are automatically sorted and organized by pressure level and month)
savedir = './savedir'
area = [50, 120, 25, 155] # N, W, S, E
variables = [
    'temperature',
    'relative_humidity'
]
years = [2020, 2021]
months = [1,2,3]
ERA.downloader(savedir, variables, years, months, area, h=850) # If h is not set, the value is treated as 'single'.

# Read
# Datetimes are given in a list. Subsequent values may be omitted.
s_datetime = 2020,1,10,12
e_datetime = 2020,3,31
temp = ERA.reader(savedir, s_datetime, e_datetime, 'temperature', h=850)
rh = ERA.reader(savedir, s_datetime, e_datetime, 'relative_humidity', h=850)
# Data can be obtained with the following accessors, respectively
print(temp.data) # datetime, values
print(temp.lat) # latitudes
print(temp.lon) # longitudes
```
