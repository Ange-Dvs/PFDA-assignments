# PFDA-assignments
This repository contains assignments for Semester 2 Programming for Data Analytics.

## Walkthrough if the assignments

This next section will walkthrough each assignment at a high level to discuss the methods and functions used. 

### Assignment 2-weather
Assignment 2 focuses on analysising and visualizing weather data using pandas and matplotlib.  
A CSV file is used to source the data and specific columns are extracted to analysis.  
The output is a plot showing the temperature recorded over time.  
Key steps:   
- Formatting:  
Timestamps are converted to a datetime format using the ``parse_dates``[^1] parameter within ``pandas.read_csv()`` function.  
- Filtering data:  
Columns to be read in from the CSV file are specified using the ``usecols`` parameter within ``pandas.read_csv()`` function.  
- Summary Statistics:  
The minimum and maximum temperatures within the dataset.  
- Visualisation:  
Temperatures recorded are plotted to show the pattern of the temperature. The x-axis intervals are set using ``mdates.HourLocator()``[^] function with the ``set_major_locator()``[^] methodto set the ticks to 2 hour intervals.  
The x-axis labels are then formatted using the ``set_major_formatter()``[^] method with the ``mdates.DateFormatter``[^] to structure the timestamp for the label in a way which is easier to read.  


### Assignment 3-domains
Assignment 3 takes in a dataset in CSV format and plots a pie chart showing the distribution across the different domains.  
- Data Processing:  
Extracting the email domain information by splitting the email column using the ``split()``[^] method to split the string at a specified character in this case it is the @ symbol.  
The   
- https://www.w3schools.com/python/matplotlib_pie_charts.asp

### Assignment 5-risk
- https://matplotlib.org/stable/gallery/pie_and_polar_charts/pie_features.html
- https://numpy.org/doc/stable/reference/generated/numpy.sort.html
- https://www.geeksforgeeks.org/plotting-multiple-bar-charts-using-matplotlib-in-python/
- https://python-graph-gallery.com/125-small-multiples-for-line-chart/
- https://www.programiz.com/python-programming/numpy/methods/tolist#:~:text=The%20tolist()%20method%20converts,changing%20its%20data%20or%20dimensions.
- https://numpy.org/doc/2.1/reference/generated/numpy.ndarray.tolist.html

### Assignment 6-weather 

- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rolling.html
- https://www.geeksforgeeks.org/python-pandas-dataframe-rolling/ 
- https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases
- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html
- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.notna.html
- https://saturncloud.io/blog/how-to-read-csv-files-as-strings-in-pandas/#reading-csv-files-as-string-type > to avoid low memory warning given
- https://www.geeksforgeeks.org/matplotlib-pyplot-margins-function-in-python/


***
End 

Author: 
Angela Davis

[^]: https://medium.com/@chanakapinfo/dealing-with-time-series-data-pandas-parse-dates-explained-5d7b28aa0f78  parse dates  
[^]: https://www.geeksforgeeks.org/matplotlib-axis-axis-set_major_locator-function-in-python/ major locator functions  
[^]: https://matplotlib.org/stable/api/dates_api.html#matplotlib.dates.HourLocator hourlocator  
[^]: https://www.geeksforgeeks.org/matplotlib-axis-axis-set_major_formatter-function-in-python/ major formatter functions  
[^]: https://matplotlib.org/stable/api/dates_api.html#matplotlib.dates.DateFormatter date formatter   
[^]
[^]
[^]
[^]
[^]
[^]
[^]
[^]
[^]
[^]
