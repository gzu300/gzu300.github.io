---
date: 15-12-2020
title: Matplotlib
---
## How to create a figure
### create a  ```figure``` instance holds the plot itself. Then use ```pyplot``` to make different kinds of plots. This is a quick way but not for complex plots with several panels.
#### Note: there is a 'current' plot concept in ```pyplot``` style. All the operations will be done on 'current' plot
```python
### Quick Matlab-style 
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
