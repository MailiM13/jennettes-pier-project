---
title: An Analysis of Bathymetric Relationships between Wave Metrics and Sand Movement
parts:
  abstract: |
    As sea levels rise and increase the rates of shoreline recession around coastal communities, developing strategies to mitigate this erosion should involve an examination of near-shore bathymetry and morphology to achieve informed management plans. This project investigates the relationship between wave energy density, height and period and changes in bathymetry.
    This analysis used bathymetric measurements of the beach surrounding the XBand radar at Jennette’s Pier and ocean conditions. It should be noted that the reliability of XBand is uncertain, so confirmation of these measurements should be applied in the future. Through a comprehensive analysis of thousands of depth measurements calculated from the XBAND radar wave measurements between December 2021 - December 2022, the designed program calculated bathymetric changes by finding differences in snapshots of bathymetry between each XBand reading and relating them to directional wave spectral measurements from an offshore Datawell Waverider buoy (CDIP 243) located at 36 0.090' (N), 75 25.254' (W), or approximately 10 miles offshore of Jennette’s Pier in Nags Head, N.C.
    This analysis revealed little correlation between wave height and the calculated volume of sand moved, though there was a slight correlation between wave energy density and volume of sand moved. These analyses suggest the value of making these measurements to make informed management decisions. 
    Future research could further identify features of the bathymetry plot associated with slower erosion rates, and enhance understanding of how swell conditions impact erosion rate. Additionally, investigating how erosion follows periodic changes across seasons and years presents an impactful avenue for analysis.
    This line of research has the potential to shape the development of artificial reefs, incorporating ecological and morphological considerations. By elucidating the relationship between wave properties and bathymetric changes, this study advances understanding, providing a starting point for future research toward mitigating shoreline recession rates as sea levels rise.
  availability: |
    Some of the data that support the findings of this study are openly available in [jennettes-pier-project] at (https://github.com/MailiM13/jennettes-pier-project/2022-2021_Xband_Data).
    The other data  that support the findings of this study are available in the CDIP historic server at (http://thredds.cdip.ucsd.edu/thredds/dodsC/cdip/archive/243p1/243p1_historic.nc.html).
---

## Introduction

Climate change has caused a rapid increase in sea level rise each year. Sea level rise has considerable negative impacts on coastal communities, where large percentages of populations reside. Sea level rise has caused property damage and led to dislocation. Increased sea levels will lead to even more disastrous effects in the future [@10.1126/science.1185782].
This pressing issue requires solutions to mitigate the erosional problems it causes. One of the current leading solutions to this on sandy beaches is beach nourishment [@10.1016/j.ocecoaman.2020.105406]. Beach nourishment is the process where the shoreline has sand pumped onto it from an offshore borrow source. However, this is not an ideal solution for several reasons. Some of these are that the sand tends to dissipate into the ocean, the process is very ecologically stressful to the surrounding environment, and it is expensive to repeat regularly.
One intriguing area that is being looked into as a solution to the problem of shoreline erosion is artificial reefs [https://doi.org/10.1016/s0964-5691(01)00048-5]. Artificial reefs are human-implanted structures that support ecological systems while controlling swells on the shoreline and potentially mitigating shoreline recession. Deploying these structures to manage shoreline recession effectively requires a strong understanding of morphodynamical and bathymetric processes, including aspects this project has looked into.
Ocean morphodynamics is the study of patterns occurring over sandbars based on related variables, including waves, currents, permanent features of the geography, and human impact. This field is very complex and, as with many fields regarding the ocean, remains enigmatic in areas that would provide a deeper understanding of this critical system of the ocean's function. Ocean morphodynamics is also a field intricately related to the function of artificial reefs, which is one reason further research could be beneficial.
This project will observe morphodynamic patterns of the swash and surf zone region. This region changes at a much higher temporal resolution than the inner shelf, allowing for more relevant data measurements and conclusions. It is also the region most easily accessed by XBand radar, the tool used to extract bathymetric values over the measurement period.
There were two main data sources for this project--the XBand radar and the CDIP buoy.
The XBand radar reads small, wind-driven waves on the ocean's surface and extrapolates that data to derive the water depth at that location [@10.1016/B978-0-12-810448-4.00007-0].
The CDIP buoy provides wave metrics like wave height and wave period, allowing calculation of wave energy.
Going into this project, the overarching question I was trying to answer was what significant features of the shoreline bathymetry resulted in the lowest shoreline erosion rate. I wanted to find this to begin research into an ideal artificial reef design and placement based on specific variables measured at the site (for example, average wave height, period, energy, longshore currents, and rip currents). The question I answered in the short term, on the path to answering this overarching question, was how wave energy, height, and period affected sand movement at a measured location. This study of ocean morphodynamics could be the first step in developing an improved system for managing shoreline erosion rates.
I hypothesized that increasing wave energy would cause an increase in the volume of sand moved over the area measured.

## Methods
### Goal of Project
This project aimed to find a quantitative relationship between various wave metrics (wave energy density, wave height, and wave period) and sand movement across a measured bathymetric location. At the end of the project, I hoped to see a strong relationship between wave energy and sand moved and build on the processes used in this project for more advanced analyses of morphodynamic relationships. These further analyses could contribute to future development in shoreline recession mitigation techniques.

### Receiving Data from XBand
The first step in analyzing the morphodynamic relationships was utilizing a source for determining bathymetric conditions. XBand Radar providedprovides depth measurements at points across a measured grid surrounding Jennette’s Pier (in a grid of approximately 1100 by 1600 meters), using a bathymetric inversion process based upon wave speed to approximate these depth measurements. The XBand Radar sweeps the radius every 55 minutes, taking 5 minutes to rotate. After reading the bathymetric conditions, the radar stores a file of thousands of values representing the water depths. These depths are calculated by measuring surface waves, which internal programs of the XBand are able to calculate depth measurements from. The radar also measures other metrics that were not directly relevant to this project. For this project, approximately a year’s worth of data was used (spanning from December 2021 to December 2022).
*Note: add github repo link with data at this section*

### Formatting XBand Data for Use
To utilize the initial XBand data describing water depth surrounding the radar, the first step was to convert the data into a 3-dimensional matrix in Python. Each timestamp where the XBand took a measurement corresponded to an array, containing the depth measurements arranged by their coordinate location. Then, the program extracted the date/time values for each recorded array and sorted them chronologically. The resulting 3-dimensional matrix was structured first by timestamps, with each containing a snapshot of the bathymetric conditions at that time, formatted in a 2-dimensional array. The resolution of this array allowed for rectangles showing the depth with an approximate size of 4.5 by 5 meters.
*Note: possibly add code snippet showing organization of matrix*

### Receiving Data from CDIP and Filtering XBand Data
The other variables necessary for this project could not be required a secondary data source. The CDIP buoy provided these variables, imported from a live server to access the values corresponding to the closest time of previously accessed XBand readings. The CDIP buoy provided wave period, wave height, information, as well as the time each data point was recorded. After receiving the CDIP values across the timespan, it was necessary to generate a separate set of values of CDIP readings that corresponded to the closest time of the reading of the XBand radar in order to determine wave conditions at the time stamp most proximate to the XBand reading.
*Note: possibly add code snippet showing server access*

### Generating Initial Representations of XBand Data
After making the XBand data usable and filtering it by wave height, it was possible to generate visual representations of the collected data. The first diagrams created were heat maps showing the depth across the measured region. The process to create this diagram was repeated at each time the filtered XBand data was available. @Bathymap-example is an example of this type of graph. After running through the entirety of the collected data, 1988 heat maps were produced.
After the initial heatmaps showing depth at each location, the next step was to generate a similar map that instead showed the change in depth over measured periods. To do this, a new array of matrices was created from the difference between each original matrix at sequential time periods. After finding this new three-dimensional array, the process of producing heat maps was replicated, but they now showed the difference in depth between two measured times. An example of this is @Delta-bathymap-example.

```{figure} images/20220104-0737.png
:label: Bathymap-example
:alt: A heatmap showing the depth of the water surrounding Jennette's Pier.
Figure shows a heatmap representing depth values across the measured region at the date-time represented in the title
```

```{figure} images/20220220-0119-20220220-0229.png
:label: Delta-bathymap-example
:alt: A heatmap showing the change in the depth of the water surrounding Jennette's Pier.
Figure shows a heatmap representing depth values across the measured region at the date-time represented in the title
```

### Extracting and Calculating Relevant Data from Sources
Once I had visual representations of the data on a primary level, I wanted to look at quantitative values extractable from the current data relevant to my question. To do this, I found the volume of sand that moved over each measured period. Finding this value required me to calculate the absolute value of the difference at each coordinate over two sequential times. Once I had that value, I calculated the volume by multiplying the depth by the amount of space it took up laterally and added that value to the running total. Repeating this process for each sequential data map resulted in a list of values showing the volume of sand moved. Also, incorporation of a function in the program to remove all NaN values from the total sand moved (these resulted from the XBand not reading depth due to insufficient wave data at that location) and associated time values, heights, and periods was necessary.
Another relevant variable to measure was the wave energy -- this was a relatively simple calculation deriving from the wave height and wave period. The 
formula $E = \left(\frac{1}{8}\right) \left(p\right) \left(g\right) * h^2$, where E $\left(\frac{J}{m^2}\right)$ is wave energy, $p$ is water density (in this case, $1027 \frac{kg}{m^3}$, as that is the average density of ocean saltwater), $g$ is the gravitational constant (rounded to $9.81 \frac{m}{s^2}$), and h is the significant wave height (in meters), provided the wave energy value for each measured interval.
Each wave energy value was then associated with the corresponding XBand time stamp.

### Generating First-Level Graphs Representing Relationships Between CDIP Metrics and Quantitative Morphodynamic Variables
After developing a quantitative variable representing one aspect of the morphodynamic process acting on the area, it was possible to relate it visually to the CDIP metrics. The first graphs were a series of boxplots describing the amount of sand moved across wave height (@wave-height-boxplot), wave period (@wave-period-boxplot), and wave energy density levels (@wave-energy-boxplot) at varying levels. The range of the levels was based on the statistical distribution of each dataset. Specifically, quartile 1, 2, and the median of wave height, wave period, and wave energy datasets were utilized as the constraints for each graph. Other graphs generated were several line plots comparing the following pairs: sand moved and wave height (@wave-height-scatter), sand moved and wave period (@wave-period-scatter) and sand moved and wave energy density (@wave-energy-scatter). These graphs allow for accessible interpretation of the relationships between measured variables.

```{figure} images/wave-height-boxplot.png
:label: wave-height-boxplot
Figure shows the distribution of sand moved at four levels of wave heights, calculated by analyzing the quartiles of the distribution of wave heights across the timespan where data was collected
```

```{figure} images/wave-period-boxplot.png
:label: wave-period-boxplot
Figure shows the distribution of sand moved at four levels of wave periods, calculated by analyzing the quartiles of the distribution of wave periods across the timespan where data was collected
```

```{figure} images/wave-energy-boxplot.png
:label: wave-energy-boxplot
Figure shows the distribution of sand moved at four levels of wave energy density, calculated by analyzing the quartiles of the distribution of wave energy density across the timespan where data was collected
```

```{figure} images/wave-height-scatter.png
:label: wave-height-scatter
Figure shows the comparison of sand moved and wave height across the measured timescale, where the x-ticks represent the date at varying intervals during this timescale
```

```{figure} images/wave-period-scatter.png
:label: wave-period-scatter
Figure shows the comparison of sand moved and wave period across the measured timescale, where the x-ticks represent the date at varying intervals during this timescale
```

```{figure} images/wave-energy-scatter.png
:label: wave-energy-scatter
Figure shows the comparison of sand moved and wave energy density across the measured timescale, where the x-ticks represent the date at varying intervals during this timescale
```

### Examining Statistical Relationships Between Wave Metrics and Bathymetry
After finding all these data sets and variables, I statistically analyzed the relationships between the variables. To do this, I performed an ANOVA test on each wave height, wave period, and wave energy at varying levels (equal to the ones described in @wave-height-boxplot, @wave-period-boxplot, and @wave-energy-boxplot) relating to the volume of sand moved. The wave period, wave height and wave energy density test all resulted in low p-values, indicating a correlation not due to chance between the variables. However, this correlation should be further studied as ANOVA tests are not necessarily the best indication of complex relationships between variables. In addition, I found the r-value of the line of best fit of the equation representing the relationship between the wave energy density and the volume of sand moved as well as the wave height and volume of sand moved.

### Generating Second-Level Graphs Representing Relationships Between CDIP Metrics and XBand Data
The final graphs generated were scatterplots incorporating a line of best fit relating wave energy density, and wave height as the independent variable and volume of sand moved as the dependent variable (@wave-height-best-fit, @wave-energy-best-fit). I found the line of best fit by incorporating a function that iterated through various function types, inputting the x and y values, and returned the one with the highest r value, allowing me to overlay the correct line of best fit over the scatterplot. This graph shows the correlation between wave energy and the volume of sand moved and has the potential to provide a method for predicting the volume of sand moved based on the line of best fit.

```{figure} images/wave-height-eq.png
:label: wave-height-best-fit
Figure shows scatterplot and line of best fit relating wave height and sand moved
```

```{figure} images/wave-energy-eq.png
:label: wave-energy-best-fit
Figure shows scatterplot and line of best fit relating wave energy density and sand moved
```

## Results
### Statistical Analysis of Wave Metric Datasets
See @Distribution-Analysis for the analysis of wave metrics and sand movement.

### Comparative Statistical Analysis of Wave Metrics as Correlated to Total Sand Moved
See @Statistical-Analysis for the comparative analysis of levels of the correlation of wave height, wave period and wave energy to total sand moved. See *figure references* for a visual analysis.

### Comparative Statistical Analysis of Equations of Best Fit Relating Wave Metrics and Total Sand Moved
See @Equatable-Relationships for the generated equations relating the amount of sand moved to wave height and wave energy density, along with the strength of these equations. See *figure references* for a visual analysis.

```{list-table} Table showing statistical analysis of wave height, wave period, wave energy and total sand moved datasets
:header-rows: 1
:name: Distribution-Analysis

* -
  - Q1
  - Median
  - Q3
  - IQR
* - Wave height $\left(m\right)$
  - 0.253
  - 0.338
  - 0.488
  - 0.235
* - Wave period $\left(s\right)$
  - 4.929
  - 5.561
  - 6.377
  - 1.448
* - Wave energy $\left(\frac{J}{m^2}\right)$
  - 116.416
  - 199.254
  - 338.125
  - 221.709
* - Total sand moved $\left(m^3\right)$
  - 67352.673
  - 158881.178
  - 508374.334
  - 441021.661
```

```{list-table} Table showing statistical analysis of wave height, wave period, wave energy and total sand moved datasets where there is an ANOVA test on each set of levels for the wave metrics
:header-rows: 1
:name: Statistical-Analysis

* -
  - P-value
  - F-statistic
  - Degrees of freedom
* - Sand moved at each wave height level
  - 7.085e-9
  - 161.940
  - 1988
* - Sand moved at each wave period level
  - 4.476e-9
  - 14.070
  - 1988
* - Sand moved at each wave energy level
  - 5.427e-29
  - 46.426
  - 1988
```

```{list-table} Table showing equation of best fit metrics and R value for the relationship between wave height, wave energy density and total sand moved
:header-rows: 1
:name: Equatable-Relationships

* -
  - Equation
  - R value
  - Strength of equation
* - Sand moved (sm) / wave height (hs)
  - $sm = 699241.300(hs) + 30310.775$
  - 0.189
  - Weak - medium
* - Sand moved (sm) / wave energy density (E)
  - $sm = \frac{12113680.910}{E}$
  - -0.655
  - Medium - strong
```

## Discussion
The outcome of this research suggests that future research is required to develop a more precise relationship between these variables and find a way of predicting between the two.
The relationship between wave period, wave height and sand moved indicates that larger waves cause more sand to move, but oddly there appears to be an inverse relationship between wave energy density and sand moved. A potential explanation for this is that waves with a higher energy tend to pass through the shore less frequently, and the sand moved could be more strongly impacted by the frequency of waves passing over. There could also be other variables entirely that are not appropriately discussed in this analysis contributing to the sand moved.
This project also provides a good baseline for incorporating XBand data with CDIP wave metrics to analyze morphodynamic patterns. There are many mediums that this could be used for in the future, such as analyzing long-term seasonal patterns, finding transverse sections of the sandbar that are most affected by waves, and other oceanic conditions that affect morphodynamic patterns (some examples of this would be longshore current, rip current, wind, etc.).
Some future areas I would like to research along this vein would be, as mentioned above, what other variables affect morphodynamic patterns and, in the long term, what specific features of bathymetry and morphodynamics could effectively reduce shoreline recession, which relates to artificial reefs.
Understanding morphodynamic patterns in coastal areas is essential for the continued well-being of coastal communities and for protecting ecosystems around the coast.

## Conclusion
The results of this study were surprising for several reasons. I hypothesized that wave energy density would have a positive correlation to the amount of sand moved, which did not prove to be true, there actually appeared to be an inverse relationship. In addition, the wave period did not have any visible correlation to total sand moved, and the correlation between wave height and sand moved was quite weak. The wave height showed a slight positive, linear correlation. The relatively low amount of data (only a year) relating wave height, period, energy, and total sand moved has room for improvement, and because the variables affecting ocean morphology are quite complex, the current models could be further refined to reflect more variables and complex relationships.