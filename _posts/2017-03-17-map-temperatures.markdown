---
layout: single
category: "software"
tags: ["map","climate"]
---

# Mapping Average Temperature

Historical data for Bangalore was downloaded from [NOAA](https://www.ncdc.noaa.gov/cdo-web/).

# Data Processing

The csv file was processed using awk:

    awk -F',' '$12 !~ -9999 { print $6","$12 }' 917368.csv | sort > sorted.csv

The temperature data contained a number of values of -9999, which we filtered out using the above awk command. The command parses out the 6th and 12th column of the csv file and sorts it by ascending date.

The data contained a number of duplicate dates which were cleaned up using [uniq.py](https://github.com/metamapblr/software/bangalore-temperature/uniq.py)

    python uniq.py

The file uniq.py takes the first date in the dataset and ignores subsequent duplicates.

The data was then processed to calculate monthly temperature averages using [month.py](https://github.com/metamapblr/software/bangalore-temperature/month.py)

    python month.py

The output data.csv is used in the [visualization](/maps/bangalore-temperatures/).
