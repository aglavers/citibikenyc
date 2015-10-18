# Data Visualization and D3.js
### Project 6 Submission - Andrew Lavers


##Summary 

The visualization can be seem at (http://aglavers.github.io/citibikenyc/)

The Citibike bike sharing service in New York City is a robust commute alternative, despite it's growing pains. This interactive chart, based on 130,000 morning rush hour trips in June 2015.

**Busiest**
The busiest departure neighborhoods are Chelsea and the Lower East with about 47,000 and 31,000 departures respectively. The least busy neighborhood is Upper East, with only 5,500 departures.

**Within the Neighborhood**
About half of Chelsea departures stay within the neighborhood compared to only 12% for the Lower East This can be seen in the far broader fan-out of the Lower East flows and the thick intra-neighborhood flow of Chelsea. Most of all rides from Brooklyn stay within the neighborhood because the Hudson River separates it from the other neighborhoods. Impressively, the remaining riders cross the Brooklyn Bridge.

**Imbalance**
The Lower East shows a strong departure/arrival imbalance with 78% of departures ending elsewhere, suggesting that it is a mostly residential neighborhood and not a work destination. Lower Manhattan is clearly more business than residential because arrivals are twice the departures, although the total rides are relatively small. Gramercy Park and Village/Soho have small gains in arrivals vs. departures.

**Bikes Gained/Lost**
The largest gainer is Lower Manhattan which ends with 93% more bikes than it starts with. The Lower East ends with 51% fewer bikes. 

##Design

#### Original design decisions

The design goals for this project were driven by the students need to learn ways to represent data flows, and a desire to learn details of D3. A data set of flows was found, the Citibike data set, and techniques for representing flows were found in the D3 examples.

The key design iterations can be seen in [index_1.html](http://aglavers.github.io/citibikenyc/index_1.html)

#### Chord layout

The earliest versions focused on [D3 Chord Layout](http://bl.ocks.org/mbostock/4062006) but this seemed to abstract for easy understanding, and the radial sizes made it harder to compare activity. A positive is  that it represents trips within a neighborhood with a flow that returns to the node, eliminating the need for duplicating.


#### Sankey layout

The change to the [D3 Sankey layout](http://bost.ocks.org/mike/sankey/) made the chart easier to comprehend, but the number of overlapping flows needed techniques to reveal the story.

The Sankey layout was chosen because it was better at representing fewer nodes and could show an ordering of nodes.

Node and flow data can also be represented on a scatter (bubble) chart with nodes on each axis and the intersection point representing the size of the flow. The Sankey layout was preferred because it more visually encodes the notion of flow and movement between the nodes. 

#### Node placement

The  vertical ordering in sankey.js was changed to ensure that nodes were always present with highest to lowest trip counts. Preserving this ordering made the base visualization easy to understand - busiest departure and busiest arrival neighborhoods in order.

#### Mouse-over visibility and color

The basic sankey layout was changed substantially to handle mouse overs and color nodes and paths simultaneously. 

- A number of **color** palettes were explored, finally settling on this [palette from colorbrewer.org](http://colorbrewer2.org/?type=qualitative&scheme=Set2&n=7). The palettes were chosen and lightened to ensure that cross over flows could still be seen without one color dominating the others. Because there are a large number of flows the more muted pastels showed more balance. 

- **Mouse over** on nodes and flows require much experimentation. The design goal was to retain the sense of interconnection while revealing information with minimal clutter. A key idea was to highlight the related  flows only, when a node is selected.

- **Tooltips** were eventually simplified based on user and instructor feedback. Switching between percentages of all and percentages relative to the neighborhood proved too confusing.

- The **full page** concept was added with an introduction to make this feel like a complete article that could stand alone

- Extensive updates to **select nodes and flows simultaneously**. This required tracking of associated nodes  
and changing the original sankey node structure

- Careful attention to **hide and reveal** using opacity. An extremely light background for counselled flows leaves a sense of the other flows being present but too light to distract the user. 

- **Transition timing **was changed many times, finally realizing that it was important to control the sequence of the hides and reveals to eliminate flicker. It was important to not revert to the full layout with all flows selected when moving from node to node because this created substantial flicker.
The code works by generating separate set of foreground and background selectors and then first applying all backgrounds selectors to fade the unselected items and then selecting the foreground to emphasize. Small details like not changing when already selected were added. 

- New **color pallette** with carefully tweaked opacity. The original color palettes had red and orange as the first colors, which dominated the charts because the the items were ordered by size. The final color palettes avoided this dominance. 

- **Labels** were placed symmetrically on outside of the nodes and titles for departures and arrivals were added adjacent to the nodes. This helped give the sankey layout a more familiar chart-axis feeling

#### Mouse-over titles (tool tips)

Mouse over titles were extended to include comprehensive flow information after feedback indicated confusion with the meaning of various percentages. After further feedback, and the addition of percentages directly on the flows, these were simplified. This is a good example of "less-is-more"

#### Percentage in nodes

Percentages were added to each of the  nodes to show relative size. 

#### Narrative

Th narrative was added to help tell the story. Once written it seemed disjoint so the idea of highlighted mouseover text words was added to connect the narrative to the chart. The idea i is to  engage the user to follow along with mouse as the story is revealed, After some trials a simple, elegant approach leveraging d3 was used. 

#### Maps and coordinates

Early ideas considered using latitude and longitude to plot the flows. Because there are many stations an  many paths between stations this proved difficult to present meaningfully and there wasn't a clear story. Summarizing trips to a neighborhood level simplified the story substantially and made it is easier to understand without the need for a map.

## Challenges with the data and decisions

Citbike is a bit like the inside of  ant colony. Thousands of short bike trips that in some ways looks like random motion, particularly in NYC, where the grid pattern makes it easy for bikes to get anywhere. It was a challenge to find the real story in the flow of the data. 

The python munge file has a few plots of other aspects of the data.

## Data Munge
As is often noted, much time went into munging and augmenting the data, even for this relatively simple data set. The data munge is in the python notebook.

Brief munge steps:

- Find zip code from latitude and longitude using geopy 

- Find neighborhood from zip code using web-scraped html file and beautiful soup.

- Determine weekday from date

- Bucket the times

## Feedback 

Key feedback received addressed confusing percentages. As a result a calculation bug was fixed and the tool tip wording was substantially improved. The feedback affirmed key conclusions.

#### Person 1
I liked the simplicity of your visualization and a interesting subject.
We can see clear which neighborhoods must be more residential or work places.
I suppose that Chelsea must be a both.
The tooltip that says 'gain/lost' just before the % of arrivals sounds onfusing to me. For instance, Chelsea have 36% of departures and 36% of arrivals, but 12% of loss. Is the loss of the 36%?

My questions raised from the data are (probably not on the scope of the project):
-> What are the population on each one?
-> Is there anything cultural that makes Lower East or Chelsea being the busiest?
-> Is there any topographical characteristics that can make those difference, for example the busiest are flat or there are hills on Lower Manhattan or Upper East?

**Action taken:** First expanded tool-tips and percentages, then simplified further,

#### Person 2 
I personally really like the grey font color. However, I had my resume in a similar color and got feedback that it was tough to read for some people.

This point is more related to the copy than the code, but do you have to mention that there are growing pains to Citibikes program? It seems odd to mention but not expand on why or how it relates to your flow chart. 

I almost missed the interactive piece of the flow layout because "Explore by moving the mouse over the departures, the arrivals, or the flows." is all the way at the bottom. I would include it in the first paragraph/blurb. Even though you mention that it is interactive, I accidentally looked over that fact so others may as well.

I think the colors are very clear and well chosen to identify each individual neighborhood. The fact that the chart shows the particular neighborhood as you hover over the name in the extra info is a nice touch.

Overall, the size of the page falls just longer than one screen (that half fold newspaper theory). I think if you got rid of the second subtitle and worked on spacing a bit, you may be able to have all of your info fit on one screen without making the viewer scroll down and would be more impactful.

**Action taken:** Moved mouse introduction to top of narrative; darkened grey slightly.

#### Person 3

Great visualization! I really like that all of the animations behave intuitively and that the tool-tips are customized for departures and arrivals. Two small things:

There a bit too much delay after mouseover before the tooltip appears. I didn't notice they were there at first.
A small map of that highlights the corresponding neighborhood on mouseover could help give a lot more context to non New York natives.

**Action taken:** Investigated the tool-tip delay but was unable to change. Implementing a map was contemplated initially but this proved very hard to do effectively.

####Person 4

- Initially the information was about neighborhoods so I wanted maps, but when I actually read the first sentence. I realized the graph on the right was perfect visualization of the data. 
- I was confused about the “Within the neighborhood” section because it mentioned “45% of Chelsea” but I didn’t see 45% for Chelsea in the graph.
- I guess my mouse affected the intensity of the colors because the Gramercy Park area was the most vivid. Might be useful to include instructions “hover over area for highlighting.”
- Should we exclude the departures that come back and arrive at the same place? Or maybe it’s useful to show for the purpose of demonstrating neighborhood busy-ness?

I learned that people take these bikes across the Brooklyn Bridge for work! Is it the farthest distance too?

**Action taken:** Percentages changed and included on links, tool-tips simplified. Instructions for mouseover moved.

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


