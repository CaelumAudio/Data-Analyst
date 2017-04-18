Summary

This is a scatter plot of 1157 baseball players. The chart graphs the Body Mass Index, which is comprised of the weight and height, of each baseball player by the number of Home Runs. If you hover over each player you will see their average and number of Home Runs of each player. The key displays the handedness of the player where R stands for Right, L stands for Left, and B stands for both. 





Design

I decided to use the baseball example provided in the project data sets; After evaluating the data I selected to represent the data in a scatter plot. I color coded the data based on handedness. 

After the feedback was received for the first graph the data is now displayed differently to improve the layout of the data. The data from the first run was not explanatory and did not show a clear finding. Now the data is easily displayed and interactive. The feedback received is listed below. The final visualization is stored in index.html. 
 
In the final visulization, index.html, the x axis is the number of Home Runs of each player. The y axis is the Body Mass Index of each player. The color portray the handedness, R = right(blue), L = left(yellow), B = both(green). The chart also has a title for clarity. 

The 3rd iteration of feedback has proved helpful in placing me on the right path to fully convey what I am trying to display. I was able to make the dots larger, remove the stroke outline, and add opacity to improve my visualization's readability. Now it looks great!




Feedback
Person 1
The data overlaps and makes it hard to understand. Because the data overlaps so heavily I am not able to draw an conclusions about the project. 
Person 2
There was some code that wasn't indented properly. It won't make a difference in terms of the code running or not running, but it's a general convention to indent code inside of tags as well as inside of functions. I marked a couple of places in the code where the indenting wasn't consistent although there are a few more spots as well. Try to keep the code indented so that it's clear what code belong to which function and which tag.

I don't really see a clear finding in this visualization. The main variables being plotted are weight and height, which look correlated although that's something generally already known and not specific to baseball players. This visualization is exploratory rather than explanatory because it plots the data "as is" rather than showing a specific, interesting finding in the data set.

In terms of the pie chart, that visualization tells me that most players in the data set are right handed followed by left handed and then both-handed. Given that there are more right handed people in the world than left handed, that isn't too surprising. Then again, we don't have information on how these players made it into the data set, so the proportion of left handed to right handed players might not mean much anyway.

To pass this part of the rubric, first do some exploratory analysis on your own to find something interesting about the data set. Then make a visualization that highlights the interesting finding in an explanatory visualization. Here are some ideas to think about:

do certain handed players tend to perform better than other handed players?
are height and/or weight (or BMI) correlated to player performance either with number of home runs or batting average?
Person 3
There is still one small problem - a typo on your introductory paragraph "players with a BMI of 260-300"
You are very nearly there here. You've put a lot of thought into making design choices that foster communication between the reader and the visualisation but it could be a bit clearer still.

Here are my suggestions:

have you tried making your circles/dots slightly larger?
if you add opacity to the dots it will be easier to see whats going in the overcrowded areas
removing the outline from the dots would also help see the patterns clearer.
the text is very small and hard to read - could you make it a little bit bigger?
did you get stuck changing the legend text and resort to the secondary legend below? As a tip, look at this section of your code:
// draw legend text
legend.append("text")
.attr("x", width - 24)
.attr("y", 9)
.attr("dy", ".35em")
.style("text-anchor", "end")
.text(function(d) { return d;})


Resources

http://bl.ocks.org/weiglemc/6185069