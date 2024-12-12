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
Temperatures recorded are plotted to show the pattern of the temperature. The x-axis intervals are set using ``mdates.HourLocator``[^] function with the ``set_major_locator()``[^] methodto set the ticks to 2 hour intervals.  
The x-axis labels are then formatted using the ``set_major_formatter()``[^] method with the ``mdates.DateFormatter``[^] to structure the timestamp for the label in a way which is easier to read.  


### Assignment 3-domains
Assignment 3 takes in a dataset in CSV format and plots a pie chart showing the distribution across the different domains.  
Key steps:  
- Data Processing:  
Extracting the email domain information by splitting the email column using the ``split()``[^] method to split the string at a specified character in this case it is the @ symbol.  
Occurences are counted for each domain using ``value_counts()``.
- Visualisation:  
A pie chart[^] is created with customised labels showing domain counts and percentage of domain occurrence within each slice. 


### Assignment 5-risk
Assignment 5 simulates 1,000 rounds of the board game Risk and analyses the attacker and defender losses.  

An extended version of the game brings dynamic army sizes ending when one side's army is wiped out with the results writen to a CSV file.
The variables ``attacker_army_size`` and the ``defender_army_size`` sets the army sizes, these numbers can be adjusted as desired.  
A ``while`` loop is used to ensure that the rounds continue until one of the army sizes drops to 0.  

>``attacker_roll_temp = np.sort(np.random.randint(1, 7, min(3, attacker_army_size)))[::-1] ``  

The numpy ``sort()``[^]function is used to sort the random numbers that are generated for the dice rolls.  
The number of rolls is set using ``min()`` to identify the smaller value between the number 3 (maximum number of rolls allowed for an attacker) or the value for attacker_army_size if that is smaller.  This is then repeated for the defended with the max set to 2.  

The last section of the notebook covers the extended scenerio which simulates battles with dynamic army sizes and stops when one side is defeated. The losses and remaining army sizes are recorded and then visualised.

>``for roll in range(min(len(attacker_roll_temp), len (defender_roll_temp)))``  

A ``for`` loop is used to iterate over the random numbers generated as dice rolls. The amount of times the rolls are compared is determined by the ``range`` class.  The ``min()`` and ``len()`` functions are then used to pick how many comparisons can be made depending on the number of rolls the attacker and defender has in that iteration as long as r is less than the min value the loop will continue.  

>``plt.plot(range(1, i), attacker_loses_per_round, label='Attacker Losses', color='orange')``  

As the number of rounds is not predictable the x-axis has to be dynamically set. To achieve this the ``range`` class is used to set the length of the x-axis staring from 1 ending in the last value set as ``i`` after the while loop finishes.  

>``writer.writerow([i, attacker_roll.tolist(), defender_roll.tolist(), attacker_loses, defender_loses, total_attacker_losses, total_defender_losses])``

The results are then written to a CSV file. 
As the number of rounds are not set the ``writerow()`` method has to be enhanced to handle varying number of rounds.  
For this ``i`` is used to select the row to write the results into in the CSV file.  
The ``tolist()``[^] method is used to convert the NumPy array for the dice rolls of the attacker and defender to better suit the format of the CSV file.  

Key steps: 

- Simulation:  
Generating random dice rolls for attackers and defenders, determining losses based on comparisons, and logging results into a CSV file.

- Visualisation:  
There are multiple methods of data visualisation utilised within this assignment.  
Within the first section of the notebook pie charts, line plots and stacked bar charts are used.  

  - Pie Chart: Shows total losses for attackers vs. defenders counted in the labels accompanied with the percentange breakdown per role.  
  The ``autopct``[^] function is used to specify how the percentage is shown and how many decimal places.

  - Line Plots: One line plot displays cumulative losses over the 1,000 rounds per role. Another shows the results of the extended version of the game, using subplots. One showing a line chart of both sides in one plot, another shows the attackers only and the last shows the defenders.

  - Stacked Bar Chart Subplots[^]: Breaks down the losses for different ranges of rounds (1–500 and 501–1000) using subplots as the number of rounds is quite large and difficult to visualise in one plot.

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
[^]: https://www.reddit.com/r/learnpython/comments/gq7jot/autopct_in_matplotlibpyplot/ autopct
[^]: https://numpy.org/doc/stable/reference/generated/numpy.sort.html numpy sort()  
[^]: https://www.geeksforgeeks.org/plotting-multiple-bar-charts-using-matplotlib-in-python/ stacked barchart  
[^]: https://www.programiz.com/python-programming/numpy/methods/tolist#:~:text=The%20tolist()%20method%20converts,changing%20its%20data%20or%20dimensions. tolist
[^]: https://matplotlib.org/stable/gallery/pie_and_polar_charts/pie_features.html pie chart explained
[^]: https://matplotlib.org/stable/gallery/pie_and_polar_charts/pie_features.html pie chart
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]:
[^]: