Python Data Science References
------------------------------
This document will show important bookmark and few explanation on code already written in the other folder and can be used as a quick cheat sheet for visual and other purpose.

``` python
print('It is a References of python 3')
```

# Data Viz with matplotlib
For jupyter notebook we can use the following code which will show the figure without writing `plt.show()` method.

``` python
import matplotlib.pyplot as plt
%matplotlib inline
```

##### Basic Command
A simple line plot can be drawn by,
``` python
plt.plot(x, y, 'r') # 'r' is the color red
plt.xlabel('X Axis Title Here')
plt.ylabel('Y Axis Title Here')
plt.title('String Title Here')
plt.show()
```
##### Creating Multiplot in same canvas
``` python
# plt.subplot(nrows, ncols, plot_number)
plt.subplot(1,2,1)
plt.plot(x, y, 'r--') # More on color options later
plt.subplot(1,2,2)
plt.plot(y, x, 'g*-');
```

##### Matplotlib Object Oriented Method
``` python
# Create Figure (empty canvas)
fig = plt.figure()

# Add set of axes to figure
axes = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # left, bottom, width, height (range 0 to 1)

# Plot on that set of axes
axes.plot(x, y, 'b')
axes.set_xlabel('Set X Label') # Notice the use of set_ to begin methods
axes.set_ylabel('Set y Label')
axes.set_title('Set Title')
```
# Data Viz with Seaborn
Seaborn is a customized visualization library on top of matplotlib. It s possible to upload example data stored in the seaborn methods. Example: `sns.load_dataset('iris')/sns.load_dataset('tips')`

##### Distribution Plots
Distribution plots are for univariate data. Also we can combine two variable in one plot the see the correlation and distribution at the both time.

```python
# simple distplot
sns.distplot(df['Column'], kde=False, bins=30)
# Distribution of bivariate data
sns.joinplot(x='Column_1', y='Column_2', data=df)
# Bi-plot can be showed as hexagonal density plots
sns.joinplot(x='ColumnName_1', y='Column_2', data=df, kind='hex')
# To Draw a regresion line
sns.joinplot(x='Column_1', y='Column_2', data=df, kind='reg')
# To draw a contor plot
sns.joinplot(x='Column_1', y='Column_2', data=df, kind='kde')
# To draw scatter plot matrix
sns.pairplot(df, hue='Categorical_Column', palette='coolwarm')
# rug plot is not that useful, works same as density plot
sns.rugplot(df['Column'])
```

##### Categorical Plots
Use to see the distribution of a categorical plot which can be refer to another numerical data.

```python
# Bar Plots
# Remember by default y axis show average of the numerical column
# To change the average the estimator parameter can be used
sns.barplot(x='Categorical_Column', y='Numeric_Column', data=df, estimator=<np.std>)
# To count the total item in each category
sns.countplot(x='Categorical_Column', data=df)
# Box PLot
sns.boxplot(x='Categorical_Column', y='Numeric_Column', data=df)
# Box Plot with hue
sns.boxplot(x='Categorical_Column', y='Numeric_Column', data=df, hue='Another_Categorical_Column')
# Violin PLot same as boxplot
sns.violinplot(x='Categorical_Column', y='Numeric_Column', data=df)
# Strip Plot
sns.stipplot(x='Categorical_Column', y='Numeric_Column', data=df, jitter=True, hue='Another_Categorical_Column', split=True)
# Swarm Plot
# Should not use for very large data set
sns.swarmplot(x='Categorical_Column', y='Numeric_Column', data=df)
# Combining Sworm and Violin
# just to write one after another
sns.violinplot(x='Categorical_Column', y='Numeric_Column', data=df)
sns.swarmplot(x='Categorical_Column', y='Numeric_Column', data=df)
# Fator Plot is the general version of all categorical plots
# Kind parameter control the type as bar, violin etc.
sns.factorplot(x='Categorical_Column', y='Numeric_Column', data=df, kind='Choose_Kind')
```
##### Matrix Plot
To create a matrix plot the data should already be in a matrix form of Cross Table. Could be a correoation matrix for example.

```python
# Heat Map
sns.heatmap(cross_table_df)
# Or we can create a pivot table the create a heatmap
trf_df = df.pivot_table(index='Column_1', columns='Column_2', values='Numerical_Column')
sns.heatmap(trf_df, cmap='magma', linecolor='white', linewidths=1)
# Then heat map can be clustered using Cluster Map
sns.clustermap(trf_df, cmap='coolwarm', standard_scale=1)
```
##### Griding in the Plot
Using griding we can take control over the mechanism of `pairplot` of seaborn.
```python
# Creating a scatter plot using PairGrid
g = PairGrid(df)
g.map(plt.scatter)
# Control the diagonal plot in scatter plot Matrix
g.map_diag(sns.distplot)
g.upper(plt.scatter)
g.map(plt.scatter)
# To show more dimension and slice we can use FacetGrid
g = sns.FacetGrid(data=df, col='Column_1', row='Column_2')
g.map(sns.distplot, 'Column_3')
# scatter plot
g.map(sns.scatter, 'Column_3', 'Column_4')
```
##### Regression Plot Seaborn
```python
# lmplot it will fit a linear fit
# use hue to sepeate by any category
sns.lmplot(x='Column_1', y='Column_2', data=df, hue='Categorical_Column')
# set marker to the plot for hue
# pass the dictionary to change even more the alpha, color etc
sns.lmplot(x='Column_1', y='Column_2',
  data=df hue='Categorical_Column', marker=['o', 'v'], \
  scatter_kws={'s':100})
# Call seperate plot by category also change the ratio and size
sns.lmplot(x='Column_1', y='Column_2',
  data=df, col='Categorical_Column', row='Another_Categorical_Column' \
  , hue='Another_Categorical_Column'
  , aspect=0.6, size=8)
```

#### Style and Color
