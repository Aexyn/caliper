# Online Results User's Guide #

## Posting Results Online ##

Go to http://microbenchmarks.appspot.com to get an API key. Paste this in your `~/.caliperrc` configuration file. With this in place, Caliper will upload the results for each benchmark you run.

## Rearranging columns ##
Click the → and ← icons in the column headers to move columns. Rearranging columns will also cause the rows to be rearranged so that values are grouped left to right. Moving the rightmost column to the right pivots the table.

## Toggle linear/logarithmic display ##
Click **linear runtime** to toggle between linear and logarithmic display. Logarithmic display is most useful when measurements span a wide range.

## Hiding Values ##
Uncheck the checkboxes in the Variables table to hide values from display.

## Renaming Runs ##
Click a run's name in the Runs table to rename it. Renames will be saved to the server.

## Interpretting Box Plots ##
When the output of a trials is subject to random variation, some barchart bars will be terminated with lighter colors and `T` lines.

![http://caliper.googlecode.com/svn/static/boxplot.png](http://caliper.googlecode.com/svn/static/boxplot.png)

The endcaps on the barcharts are [Box Plots](http://mathworld.wolfram.com/Box-and-WhiskerPlot.html), and are composed of up to 5 values:
  1. The left-side `T` indicates the **minimum** measured value.
  1. The left-hand edge of the lighter-colored sections is the **first quartile**. 25% of the measurements are below this value; 75% are above it.
  1. The middle edge that divides the two lighter-colored sections is the **median**. 50% of the measurements are below this value; 50% are above it.
  1. The right-hand edge of the lighter-colored sections is the **third quartile**. 75% of the measurements are below this value; 25% are above it.
  1. The right-side `T` indicates the **maximum** measured value.

Many bars will not have all of these features. In that case, the omitted feature is _not interesting_: it is equal to the adjacent value. If all measurements are exactly equal, then the minimum, first-quartile, median, third-quartile and maximum will all be together at the bar's end.

Variation may be due to the way the benchmark was coded. For example, use of a `java.util.Random` within the benchmark can yield unrepeatable results. Variation may also come from uncontrollable factors in the underlying operating system and hardware. For example, benchmarks that use large amounts memory will be impacted by behind-the-scenes caches and paging.