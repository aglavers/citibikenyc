# Data Visualization and D3.js
### Project 6 Submission - Andrew Lavers


##Summary 

The visualization can be seem at (http://aglavers.github.io/citibikenyc/)

The Citibike bike sharing service in New York City is a robust commute alternative, despite it's growing pains. This interactive chart, based on 130,000 morning rush hour trips in June 2015.

**Busiest**
The busiest departure neighborhoods are Chelsea and the Lower East with about 47,000 and 31,000 departures respectively. The least busy neighborhood is Upper East, with only 5,500 departures.

**Within the Neighborhood**
About 45% of Chelsea departures stay within the neighborhood compared to only 12% for the Lower East This can be seen in the far broader fan-out of the Lower East flows and the thick intra-neighborhood flow of Chelsea. 63% of all rides from Brooklyn stay within the neighborhood because the Hudson River separates it from the other neighborhoods. Impressively, the remaining riders cross the Brooklyn Bridge.

**Imbalance**
The Lower East shows a strong departure/arrival imbalance with 78% of departures ending elsewhere, suggesting that it is a mostly residential neighborhood and not a work destination. Lower Manhattan is clearly more business than residential because arrivals are twice the departures, although the total rides are relatively small. Gramercy Park and Village/Soho have small gains in arrivals vs. departures.

**Bikes Gained/Lost**
The largest gainer is Lower Manhattan which ends with 93% more bikes than it starts with. The Lower East ends with 51% fewer bikes. 

##Design
#### Original design decisions

The design goals for this project were driven by the students need to learn ways to represent data flows, and a desire to learn details if D3. This is a little different than what a real project might be where a presentation should be chosen that is appropriate for the data.

Given this choice, a data set of flows was sought, finally settling on the Citibike data set.

The design iterations can be seen in [index_1.html](http://aglavers.github.io/citibikenyc/index_1.html)

#### Chord layout

The earliest versions focused on [D3 Chord Layout](http://bl.ocks.org/mbostock/4062006) but this seemed to abstract for easy understanding, and the radial sizes made it harder to compare activity. A positive is  that it represents trips within a neighborhood with a flow that returns to the node, eliminating the need for duplicating.


#### Sankey layout

The change to the [D3 Sankey layout](http://bost.ocks.org/mike/sankey/) made the chart easier to comprehend, but the number of overlapping flows needed techniques to reveal the story.

#### Mouse-over visibility and color

The basic sankey layout was changed substantially to handle mouse overs and color nodes and paths simultaneously. A number of color palettes were explored, finally settling on this [palette from colorbrewer.org](http://colorbrewer2.org/?type=qualitative&scheme=Set2&n=7).

#### Mouse-over titles (tool tips)

Mouse over titles were extended to include comprehensive flow information after feedback indicated confusion with the meaning of various percentages.


#### Telling the story

The narrative was added, in the style of a news article, with the addition of live-link colored words.


## Challenges with the data and decisions

Citbike is a bit like the inside of  ant colony. Thousands of short bike trips that in some ways looks like random motion, particularly in NYC, where the grid pattern makes it easy for bikes to get anywhere. It was a challenge to find the real story in the flow of the data. 

The python munge file has a few plots of other aspects of the data.

## Data Munge
As is often noted, much time went into munging and augmenting the data, even for this relatively simple data set. The data munge is in thepython notebook.

Brief munge steps:

- Find zip code from latitude and longitude using geopy 

- Find neighborhood from zip code using web-scraped html file and beautiful soup.

- Determine weekday from date

- Bucket the times

## Feedback 

Key feedback received addressed confusing percentages. As a result a calculation bug was fixed and the tool tip wording was substantially improved. The feedback affirmed key conclusions.

## Resources

#### D3 Chord layout
http://bl.ocks.org/mbostock/4062006

For early versions

#### D3 Sankey layout
http://bost.ocks.org/mike/sankey/

For the final layout. The index.html was based heavily on this example using much of the code. The code was extended substantially to handle mouseovers, to color flows, to label axes and  many other small details. 

This includes **`sankey.js`**, submitted as **`citibikenyc.js`** with only one line of code changed to ensure vertical ordering of nodes by size.

#### Citibike NYC - information and data
http://www.citibikenyc.com/
http://www.citibikenyc.com/system-data

#### Color Palettes
http://colorbrewer.org

#### D3
http://d3js.org

Documentation and Examples

#### Beautiful Soup
http://www.crummy.com/software/BeautifulSoup/

Parsing html for neighborhood/zip tables

#### Stack Overflow
http://stackoverflow.com

#### Hosting pages on git
http://blog.teamtreehouse.com/using-github-pages-to-host-your-website

#### ggplot for early data exploration
https://github.com/yhat/ggplot/

####  A few of the many smaller sites referenced for details

Referenced many articles for small coding tips, bug resolution etc.

http://www.w3schools.com/tags/tag_span.asp

http://stackoverflow.com/questions/13379912/javascript-summing-arrays-using-d3-nest


