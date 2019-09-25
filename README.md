# polypatch

Given a plot of Y vs X, select an interval of X and fit a polynomial to the data. Optionally, select a sub-interval of X to be ignored by the fit.

The code forces the fit to pass through the two last and two first data point in the selected interval. This, in order to achieve a smoother mathing between the data and the fit. As a result, the degree of the fit must be 3 or higher. This is done by means of Lagrangemultipliers.

The plots are generated by the Python package Matplotlib that provides interactive tools like zooming, dragging, and rescaling, which are all useful for data exploration.

## Example 1

![alt text](https://github.com/stefano-rgc/polypatch/blob/master/exemplary_images/example.gif)

Short explanation of the figure:

1. It uses the left button of the mouse to select the interval to be considered for the fit (red curve).
2. It uses the right button of the mouse to select the interval to be excluded from the fit (black vertical lines).
3. It performs the polynomial fit by selecting a degree and then clicking the button on the screen (green curve).

**To enable recognition of the left and right buttons, first hit enter**

After closing the windows, the following summary will be displayed on the console:

```
=========================================
Interval for the fit:
xmin = 0.0143, 	xmax_fit = 0.0313
=========================================
Interval excluded from the fit:
xmin = 0.0192, 	xmax = 0.0252
=========================================
Polynomial degree of the fit = 3
=========================================
```

Run the program
Make sure you are using Python3 and have installed the following Python packages:

- Numpy (https://www.numpy.org/)
- Matplotlib (https://matplotlib.org/)

To reproduce the example, execute the following lines in within Python:

```Python3
import numpy as np
import matplotlib.pyplot as plt
from polypatch import polypatch

# Sample data
x = np.arange(0.25,1.50,0.01) 
sigma=0.05; mu=1
gaussian = 1/(sigma*np.sqrt(2*np.pi))*np.exp(-(x-mu)**2/(2*sigma**2) )
y = 1 + 0.5*x - x**2 + 0.5*x**3 + 0.1*gaussian 
        
# Making a plot  
figure = plt.figure()  
axes = plt.axes()
axes.set_title('Example')
axes.set_ylabel('Y data')
axes.set_xlabel('X data')
line2d, = plt.plot(x,y) # Mind the comma!                                           
 
# Fitting a polynomial interactively
mask, fit = polypatch(figure, axes, line2d)

# Integration of the fit values into the original data
y_modified = y.copy()
y_modified[mask] = fit

# Plot original data and modified data
figure = plt.figure()  
axes = plt.axes()
axes.set_title('Example')
axes.set_ylabel('Y data')
axes.set_xlabel('X data')
plt.plot(x,y,label='original data', color='black')
plt.plot(x,y_modified,label='modified data', color='red')
plt.legend(loc='best')
plt.show()
```

Extra documentation can be accessed from within Python via

```
>>> help(polypatch)
```

## Example 2

The program also allows for in situ comparison of polynomial fits of different degree.

![alt text](https://github.com/stefano-rgc/polypatch/blob/master/exemplary_images/example2.gif)

Short explanation of the figure:

1. Same as the example 1, however, this time the check box needs to be clicked
