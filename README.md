# polypatch

Given a Matplotlib plot of Y vs X, select an interval of X and fit a polynomial to the data. Optionally, select a sub-interval of X to be ignored by the fit.

The code forces the fit to pass through the two last and two first data point in the selected interval. This, in order to achieve a smoother mathing between the data and the fit. As a result, the degree of the fit must be 3 or higher. This is done by means of Lagrangemultipliers.

The Matplotlib figure used as input can contain a legend, title, labels, etc.

![alt text](https://github.com/stefano-rgc/glitch_add_and_remove/blob/master/exemplary_images/remove_glitch.gif)
