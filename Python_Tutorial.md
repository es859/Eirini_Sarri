```python

  from aguaclara.core.units import unit_registry as u
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  from scipy import stats

  #Now we create a pandas dataframe with the data in the file
  df = pd.read_csv('C:/Users/Eirini Sarri/Desktop/Linear_Data_Set.csv')

  print(df)

  # The column headers can be access by using the list command
  list(df)
  columns = df.columns
  print(columns)


  # Use the iloc command and select all of the rows in column 0.
  x = df.iloc[:,0].values * u.degK

  # Use the iloc command and select all of the rows in column 1.
  y = df.iloc[:,1].values * 1/u.sec

  # We will use the stats package to do the linear regression.
  # It is important to note that the units are stripped from the x and y arrays when processed by the stats package.
  slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)
  slope

  #We can add the units to intercept by giving it the same units as the y values.
  intercept = intercept * y.units
  # Note that slope is dimensionless for this case, but not in general!
  # For the general case we can attach the correct units to slope.
  slope = slope * y.units/x.units

  # Now create a figure and plot the data and the line from the linear regression.
  fig, ax = plt.subplots()
  # plot the data as red circles
  ax.plot(x, y, 'ro', )

  #plot the linear regression as a black line
  ax.plot(x, slope * x + intercept, 'k-', )

  # Add axis labels using the column labels from the dataframe
  ax.set(xlabel=list(df)[0])
  ax.set(ylabel=list(df)[1])
  ax.legend(['Measured', 'Linear regression'])
  ax.grid(True)

  plt.savefig('C:/Users/Eirini Sarri/github/Plot_Lab_1')
  plt.show()  

print(slope,intercept)

```

$$y=0.685*x-185.6$$
