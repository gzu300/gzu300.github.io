---
date: 15-12-2020
title: Matplotlib
---
## set backends for different usecases
### *Always set backends at the top before importing and plotting*
### set backends for different use cases. Usually ```notebook``` for interactive scenario like jupyter notebook or shell. ```inline``` for static plots for applications. 
Other backend such as ```qt``` is to embed with GUIs.
```python
import matplotlib
matplotlib.use('qt5agg') #when wrong argument given, a list of arguments will be given in the error msg.
```
### magic functions in IPython
```python
%matplotlib inline # or notebook
import matplotlib.pyplot as plt
```
## structure
### ```Figure``` object
This is the object that keeps track all the ```axes```. Typically one ```Figure``` object contains many ```Axes``` objects. An empty ```Figure``` can be created explicitly by ```plt.figure()``` and add ```Axes``` by ```add_subplots()```
```python
import matplotlib.pyplot as plt

#first way
fig = plt.figure()
ax = fig.subplots() #this add one Axes to the figure
ax.plot(...)

#second way: create one plot
fig, ax = plt.subplots()
ax.plot(...)
#third way
fig, (ax1, ax2) = plt.subplots(1,2)
for each in [ax1, ax2]:
  each.plot(...)
  
#forth way
fig = plt.figure()
gs = fig.add_gridspec(2,2)
ax1 = fig.add_subplot(gs[0,0]) # takes [0,0] position
ax2 = fig.add_subplot(gs[0,1]) # takes [0,1] position
ax3 = fig.add_subplot(gs[1,:]) #takes the whole second row
ax1.plot(...)
ax2.plot(...)
...
```
### ```Axes``` object
- This is what you think of as 'a plot', it is the region of the image with the data space. 
- ```Axes``` has set methods for ticks, x/y limits, titles, etc.
- ```Axes``` also has 2 or 3 ```Axis``` objects which control axies in ```Axes```
- check api for detailed methods
### ```Axis``` object ```Text``` ```Patch``` etc. Check API when necessary
### ```Artist``` object
The most lowlevel object, all the objects that can be shown in the image is the child of ```Artist```
### ```twinx()``` method
Add a second y axis. Example:
```python
fig, ax = plt.subplots()
ax.plot(...)
ax2 = ax.twinx() #this will add a second y axis
```

## How to create a figure
### create a  ```figure``` instance holds the plot itself. Then use ```pyplot``` to make different kinds of plots. This is a quick way but not for complex plots with several panels.
#### Note: there is a 'current' plot concept in ```pyplot``` style. All the operations will be done on 'current' plot
### pyplot style
```python
### Quick Matlab(pyplot)-style 
plt.figure()
plt.plot()
plt.axis([xmin, xmax, ymin, ymax])
plt.title('')
dir(plt) # see more methods 
### Matlab-stype with subplots
plt.subplot(2,1,1)
plt.plot()
plt.subplot(2,1,2)
plt.plot()
```
### OO-style plot. ```plt.subplots``` will create figure object and the axes. axes is a numpy array which is a matrix specifies the location.
#### ```fig``` is the same as instance by ```plt.figure()```. ```ax``` holds all the subplot instances. We can switch easily between subplots
```python
### OO-style
fig, ax = plt.subplots(6) # create a flat array of subplots
fig1, ax1 = plt.subplots(3,3) #create a 3x3 array of subplots, in total 9 subplot instances
ax[0].plot() #plot something on ax[0] subplot
ax[0].plot() #plot somethine else on ax[0]
ax[2].plot() #plot on ax[2]
ax[0].set_xlim() #This will not change 'current' plot. see below.
plt.plot()   #this will always plot on 'current' plot, which might be the last plot.
dir(ax) # see more methods
...
```
#### conventions of ```plot``` method. 
```fmt = '[marker][line][color]```
```python
fmt = '.r--' # point, red dashed line
plt.plot(x, y, fmt)
plt.scatter() #similar to plot(). but it is more refined
```
## Events(interactivity) driven plots.
