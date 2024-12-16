# PFDA-assignments
This repository contains assignments for Semester 2 Programming for Data Analytics.

## Cloning repository from GitHub

1. Copy the following URL:
https://github.com/Ange-Dvs/PFDA-assignments.git

2. Open CMDER or if using VS Code open the terminal pane

3. Navigate to the folder where you want to clone the repository to on your machine and type git pull
``git clone https://github.com/Ange-Dvs/PFDA-assignments.git``

4. Set merge as the mode for the pull
``git config pull.rebase false``

5. Initiate the pull of the GitHub repository
``git pull``

6. If the pull has been successful, you should see 6 files pulled from GitHub. The ``readme.md``, the ``.gitignore`` file, the 4 assignments contained within individual Jupyter notebooks and two ``CSV`` files which were generated as a result of running the ``assignment_05_risk.ipynb`` notebook before the final push to GitHub.

## Software used
The software used for the creation of the assignment notebooks included VS Code, Python, Jupyter notebooks & GitHub. 

## Walkthrough if the assignments
This next section will walkthrough each assignment at a high level to discuss the steps taken within each. 

### Assignment 2-weather
Assignment 2 focuses on analysing and visualizing weather data using ``Pandas`` and ``Matplotlib``.  
A ``CSV`` file is pulled from GitHub to source the data and specific columns are extracted to analysis.  
In this step, the ``reportStartDateTime`` column is converted to a NumPy datetime64 object.[^1]
The output is a plot showing the temperature recorded over time. 

Key steps:   
- Formatting:  
Timestamps are converted to a datetime format using the ``parse_dates``[^2] parameter within ``pandas.read_csv()`` function.  

- Filtering data:  
Columns to be read in from the ``CSV`` file are specified using the ``usecols`` parameter within ``pandas.read_csv()`` function.  
- Summary Statistics:  
The minimum and maximum temperatures within the dataset are calculated.  
- Visualisation:  
Temperatures recorded are plotted to show the pattern of the temperature. The x-axis intervals are set using ``mdates.HourLocator``[^3] function with the ``set_major_locator()``[^4] method to set the ticks to 2 hour intervals.  
The x-axis labels are then formatted using the ``set_major_formatter()``[^5] method with the ``mdates.DateFormatter``[^6] to structure the timestamp for the label in a way which is easier to read.  

### Assignment 3-domains
Assignment 3 takes in a dataset in ``CSV`` format and plots a pie chart showing the distribution across the different domains.  

Key steps:  
- Data Processing:  
Extracting the email domain information by splitting the email column using the ``split()``[^7] method, to split the string at a specified character. In this case it is the '@' symbol.  
Occurrences are counted for each domain using ``value_counts()``.

- Visualisation:  
A pie chart[^8] is created with customised labels showing domain counts and percentage of domain occurrence within each slice.  
They Python ``.index()``[^9] method is used to take the domain names from the ``domain_counts`` series automatically, adding the percentage per each value in the slice and adding a shadow to the chart.

### Assignment 5-risk
Assignment 5 simulates 1,000 rounds of the board game Risk and analyses the attacker and defender losses.  

An extended version of the game brings in the possibility of setting dynamic army sizes, ending when one side's army is wiped out with the results written to a ``CSV`` file and visualised using a line plot.  
The variables ``attacker_army_size`` and the ``defender_army_size`` sets the army sizes, these numbers can be adjusted as desired.

A ``while`` loop is used to ensure that the rounds continue until one of the army sizes drops to 0.  

>``attacker_roll_temp = np.sort(np.random.randint(1, 7, min(3, attacker_army_size)))[::-1] ``  

The ``NumPy ````sort()``[^10]function is used to sort the random numbers that are generated for the dice rolls.  
The number of rolls is set using ``min()`` to identify the smaller value between the number 3 (maximum number of rolls allowed for an attacker) or the value for attacker_army_size if that is smaller.  This is then repeated for the defender with the maximum number of rolls set to 2.  

>``for roll in range(min(len(attacker_roll_temp), len (defender_roll_temp)))``  

A ``for`` loop is used to iterate over the random numbers generated as dice rolls. The amount of times the rolls are compared is determined by the ``range`` class.  The ``min()`` and ``len()``[^11] functions are then used to pick how many comparisons can be made depending on the number of rolls the attacker and defender has in that iteration as long as ``r`` is less than the ``min`` value the loop will continue.  

>``plt.plot(range(1, i), attacker_loses_per_round, label='Attacker Losses', color='orange')``  

As the number of rounds are not predictable the x-axis has to be dynamically set. To achieve this the ``range`` class is used to set the length of the x-axis staring from 1 ending in the last value set as ``i`` after the while loop finishes.  

>``writer.writerow([i, attacker_roll.tolist(), defender_roll.tolist(), attacker_loses, defender_loses, total_attacker_losses, total_defender_losses])``

The results are then written to a ``CSV`` file. 
As the number of rounds are not set the ``writerow()`` method has to be enhanced to handle varying number of rounds.  
For this ``i`` is used to select which row to write the results into in the ``CSV`` file.  
The ``tolist()``[^12] method is used to convert the ``NumPy`` array for the dice rolls of the attacker and defender to better suit the format of the ``CSV`` file.  

Key steps: 

- Simulation:  
Generating random dice rolls for attackers and defenders, determining losses based on comparisons, and logging results in a ``CSV`` file.

- Visualisation:  
There are multiple methods of data visualisation utilised within this assignment.  
Within the first section of the notebook pie charts, line plots and stacked bar charts are used.  

  - Pie Chart: Shows total losses for attackers vs. defenders counted in the labels, accompanied with the percentage breakdown per role.  
  The ``autopct``[^13] function is used to specify how the percentage is shown and with how many decimal places.

  - Line Plots: One line plot displays cumulative losses over the 1,000 rounds per role. Another shows the results of the extended version of the game, using subplots. One showing a line chart of both sides in one plot, another shows the attackers only and the last shows the defenders.

  - Stacked Bar Chart Subplots[^14]: Breaks down the losses for different ranges of rounds (1–500 and 501–1000). Subplots used as the number of rounds are quite large and difficult to visualise in one plot.

### Assignment 6-weather 

This assignment involves analysis of weather data using ``Pandas`` Time Series [^15], focusing on temperature and windspeed trends.  
The dataset is resampled to different frequencies (daily and monthly)[^16] to compute mean values, rolling averages, and maximum values. 

The data is read in through the ``read_csv()`` function. ``low_memory=False``[^17] is specified to aviod warnings working with the dataset due to inconsistent datatypes in the columns and the large amount of data contained within the ``CSV`` file.  The first 23 rows of the file are also skipped as they contain extra information which is not relevant for the assignment and caused issue when reading in using the ``CSV`` format. The skipping of the rows is done using ``skiprows=23``.  

>``df['date'] = pd.to_datetime(df['date'], format='%d-%b-%Y %H:%M',dayfirst=True)``

The date column is converted to datetime using ``Pandas`` ``to_datetime()`` function[^18].  

>``df['wdsp'] = pd.to_numeric(df['wdsp'], errors='coerce')``

The windspeed column is then converted to numeric using ``Pandas `` ``to_numeric``[^19] function to handle any invalid data such as blank entries. ``errors='coerce'`` is used to parse any invalid values to ``NaN``. 

>``df.set_index('date', inplace=True)``

Then the date is set as the DataFrame index[^20] to allow for easier filtering and performing operations on the dataset based on the time and date.

Some plots of the temperature data are generated. The data is resampled using the ``ME``offset alias[^21] to a monthly frequency. The monthly mean is determined and displayed as a line plot.

>``rs_mean_month = rs_mean_month[rs_mean_month['temp'].notna()]`` 

The resampled monthly data is filtered to ensure there are no rows where with ``NaN`` in the temperature column [^22]. 

The focus then switches to the windspeed column.

>``no_of_blanks_in_wdsp = df['wdsp'].isna().sum()``

First the column is checked to count the amount of blank entries in the dataset for the windspeed column, using ``Pandas`` ``isna()``[^23] method combined with the ``sum()`` method. 

>``df = df[df['wdsp'].notna()]``

The dataset is then filtered by dropping the rows that have blank values in the windspeed column. 

The number of blank entries are then checked again and displayed for the user.
The windspeed data is displayed using a line plot, resampled and various calculations are performed. 

>``df['wdsp_rolling_24h'] = df['wdsp'].rolling(window='24h').mean()``

The mean rolling windspeed for 24 hour window is determined using ``Pandas`` ``rolling()``[^24] and ``mean()``.

The windspeed data is resampled to a monthly frequency and the mean calculated again. 
The daily max windspeed is then determined by resampling the data again to a daily frequency and picking the max of each day using ``max()`` method. 

The daily max windspeed data is resampled again to monthly intervals to show the monthly mean of the daily max windspeed information. This is then plotted using a line plot. 

Key steps:

- Data Preparation:   
The date column is converted to datetime series and set as the DataFrame index. The dataset is cleaned and missing values are removed before plotting.

- Analysis:

  - Daily and monthly mean temperatures calculated. 
  - 24-hour rolling averages shown to visualise trends in windspeed.
  - Resampling data to calculate monthly averages of rolling windspeed and daily maximum windspeed trends.

- Visualization:
  - Line plots for temperature trends (daily and monthly).
  - Rolling mean windspeed trends and monthly averages.
  - Daily maximum windspeed and its monthly mean trends.

## Libraries used 

Within the assignments various libraries are used including: 
- ``Pandas``
- ``Matplotlib.pyplot``
- ``Matplotlib.dates``
- ``NumPy``
- ``Seaborn``
- Built-in/Standard library


<font size="4"><b>Pandas</b></font>   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Pandas` is a library in Python used for data analysis which enables the use of two-dimensional tables called DataFrames.  
Within the assignments the ``Pandas`` library is used to read in the data from the various ``CSV`` files.  
It is also used to convert date information in the ``CSV`` file to a datetime series.

The following are methods used throughout the assignments from `Pandas`: 

> ``.read_csv`` (Function) - Reads a CSV file into a DataFrame.[^25]

> ``.value_count`` (Method) - Counts unique values in a Series and returns their frequencies.  

> ``.items`` (Method) - Iterates over DataFrame columns as key-value pairs.  

> ``.to_datetime`` (Function) - Converts a string or other formats to a ``datetime`` object.  

> ``.to_numeric`` (Function) - Converts a Series to numeric types, coercing errors if specified.  

> ``.set_index`` (Method) - Sets a DataFrame column as the index.

> ``.resampled`` (Method) - Resamples time-series data to a different frequency.  

> ``.mean`` (Method) - Calculates the mean of values along a DataFrame or Series axis.

> ``.notna`` (Function) - Detects non-missing values in a Series or DataFrame.

> ``.isna`` (Function) - Detects missing values in a Series or DataFrame.

> ``.rolling`` (Method) - Provides rolling window calculations for time-series data.

<font size="4"><b>Matplotlib.pyplot</b></font>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The ``Matplotlib.pyplot`` library is used for visual representation of the dataset.
This library enables the creation of many types of plots including line plots, pie charts and bar charts which are generated throughout the assignments.  
There is a high-level of customisation possible with options to switch up the colour, markers, legend, labels and titles of the plots.

The following are methods used from `Matplotlib.pyplot`: 

> ``.pie`` (Function) - Creates a pie chart to display proportions or percentages for different categories. 

> ``.legend`` (Function) - Adds a legend to a plot to label the data.

> ``.title`` (Function) - Add a title to a plot, the title can be customised to alter how the font looks (weight and size) and location on the plot.

> ``.show`` (Function) - Used after the plot has been created to show the plot.

> ``.grid`` (Function) - Can be used to add or remove gridlines from the plot to enhance readability of the plot. 

> ``.bar`` (Function) - Create a bar chart to display categorical data.

> ``.margins`` (Function) - Adjusts the padding around the data in a plot for neater plots.

> ``.tick_params`` (Function) - Customises the appears of ticks on axes of a plot. Aspects like size, colour and position can be set using this function. 

> ``.plot`` (Function) - Create a line plot by default. It can also be adapted for a variety of visualizations by adjusting its parameters.

> ``.subplot`` (Function) - Supports the creation of multiple plots in one figure. The number of plots which can be displayed is controlled by values entered for the number of columns and rows required. 

> ``.xticks`` & ``.yticks`` (Function) - Offers the ability to change the default tick settings on the x and y axes including the possibility to change the position of the ticks on the plot borders or remove the ticks completely.

> ``.xlabel`` & ``.ylabel`` (Function) - Sets the heading for the axes and allows customisation of the font with the possibility to change the style, font and location of the labels.

> ``.xlim`` (Function) - Sets limit of the x-axis. This is useful when it's needed to overwrite the default value or range for the axes.

> ``.figtext`` (Function) - Adds text to plots.

> ``.figure`` (Function) - Create a new figure object, holding all elements of a plot, such as axes, titles, legends, and other visual elements. The size of the figure can also be specified within the ``.figure`` function.

<font size="4"><b>NumPy</b></font>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``NumPy`` is used in the assignments to facilitate calculations on the large amount of data. When working with datasets ``NumPy`` is useful for its ability to handle arrays and possibility to complete mathematical calculation and sorting.

> ``.sort`` (Function) - Sorts an array in either ascending or descending order depending on what is specified.  Returns a sorted copy of the array.

> ``.random`` (Module) - A submodule of ``NumPy`` that contains functions for generating random numbers, sampling, and creating random arrays. The ``.randint``function from ``.random`` is used for generating a random set of integer.  

<font size="4"><b>Seaborn</b></font>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``Seaborn`` is used for advanced data visualization and statistical analysis.
This library builds on ``Matplotlib``, offering a more user-friendly interface and aesthetically pleasing default styles for plots such as heatmaps, scatterplots, and boxplots.  
There is a high level of customization available, with options to easily manage colour palettes, adjust axes styling, add statistical annotations, and create visually appealing multi-plot grids.

> ``.sns.lineplot`` (Function) - Creates a line plot for data visualization.  

<font size="4"><b>Default Python Functionality (Built-in or Standard Library)</b></font>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The built-in Python functionality and standard library provide tools for data manipulation and processing.
These features include operations like sorting, summing, and string manipulation, which are frequently applied throughout the assignments.
They offer a straightforward and efficient way to handle core programming tasks without requiring external libraries.

>``split`` (Method) -  Splits a string into a list using a specified delimiter (default is whitespace).  

>``.min`` (Function) - Returns the smallest value in an iterable or among arguments.

>``.max`` (Function) - Returns the largest value in an iterable or among arguments. 

>``.sum`` (Function) - Returns the sum of values in an iterable.  

>``.writerow`` (Method from `csv` module) - Writes a single row to a ``CSV`` file.  

>``.csv.writer`` (Class from `csv` module)  - Creates an object for writing to ``CSV`` files.

>``.append`` (Method) - Adds an element to the end of a list.

>``.tolist`` (Method) - Converts an array-like object to a Python list.

***
End 

**Author:**   
Angela Davis

[^1]: https://numpy.org/doc/2.1/reference/arrays.datetime.html
[^2]: https://medium.com/@chanakapinfo/dealing-with-time-series-data-pandas-parse-dates-explained-5d7b28aa0f78  
[^3]: https://matplotlib.org/stable/api/dates_api.html#matplotlib.dates.HourLocator
[^4]: https://www.geeksforgeeks.org/matplotlib-axis-axis-set_major_locator-function-in-python/ 
[^5]: https://www.geeksforgeeks.org/matplotlib-axis-axis-set_major_formatter-function-in-python/
[^6]: https://matplotlib.org/stable/api/dates_api.html#matplotlib.dates.DateFormatter
[^7]:https://www.w3schools.com/python/ref_string_split.asp
[^8]: https://matplotlib.org/stable/gallery/pie_and_polar_charts/pie_features.html
[^9]: https://www.w3schools.com/python/ref_string_index.asp#:~:text=Definition%20and%20Usage,the%20value%20is%20not%20found.
[^10]: https://numpy.org/doc/stable/reference/generated/numpy.sort.html
[^11]: https://www.w3schools.com/python/ref_func_len.asp
[^12]: https://www.programiz.com/python-programming/numpy/methods/tolist#:~:text=The%20tolist()%20method%20converts,changing%20its%20data%20or%20dimensions.
[^13]: https://www.reddit.com/r/learnpython/comments/gq7jot/autopct_in_matplotlibpyplot/
[^14]: https://www.geeksforgeeks.org/plotting-multiple-bar-charts-using-matplotlib-in-python/
[^15]: https://pandas.pydata.org/docs/user_guide/timeseries.html
[^16]: https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#resampling
[^17]: https://www.geeksforgeeks.org/pandas-read_csv-low_memory-and-dtype-options/
[^18]: https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html
[^19]: https://pandas.pydata.org/docs/reference/api/pandas.to_numeric.html#pandas-to-numeric
[^20]: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.set_index.html
[^21]:https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases
[^22]: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.notna.html
[^23]: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.isna.html
[^24]: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rolling.html
[^25]: https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html