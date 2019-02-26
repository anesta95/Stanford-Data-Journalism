# Stanford-Data-Journalism
## Public Affairs Data Journalism Stanford Class

### This is my **initial** posting on GitHub following along with the _Public Affairs Data Journalism Course_ from Stanford.

The first assignment from [this link](http://www.padjo.org/2014-09-23/#homework-details) was to post something in markdown on my README master branch. ~~Hopefully I don't screw this up~~

I am hoping that this course will help me refine both my data analysis and journalistic skills. I anticipate writing a good amount of `code`, but also sharpening my story-finding and story-telling instincts. 

More tangibly, while I shadow this course I am looking to accomplish these tasks:
-Develop a mastery of Excel for data cleaning and analysis.
-Obtain a working knowledge of at least one maping software.
-Achieve a comfort with the GitHub interface so that I can use it for other individual projects.
-Manage databases in a coherent and useful way.

I am working to make this the beginning of a long and fruitful career. One of the most powerful things I already learned from the first lesson in the course was this from Nate Silver's ["What the Fox Knows"](http://fivethirtyeight.com/features/what-the-fox-knows/)
>You may have heard the phrase the plural of anecdote is not data. It turns out that this is a misquote. The original aphorism, by the political scientist Ray Wolfinger, was just the opposite: The plural of anecdote is data.
>Wolfinger’s formulation makes sense: Data does not have a virgin birth. It comes to us from somewhere. Someone set up a procedure to collect and record it. Sometimes this person is a scientist, but she also could be a journalist.

Here is to my Data Journalism journey!

### For the class titled "Big Bad Data" I was asked to examine the DUI and Kidnapping data from San Francisco between 2003 and 2013 to answer this question:

>If it were true that Uber’s launch in San Francisco in June 2010 had a noticable impact on DUI reports, then we expect to see (this or that) in (yadda yadda yadda) kind of comparison. As the data shows, we (do/do not).

I ended up not using the Excel spreadsheet that was provided and went straight to the City of San Francisco's Data Website to gather their Police Department's [Incident Report](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-Historical-2003/tmnf-yvry) for every recorded DUI, Adult Kidnapping, and Traffic Violation from 2003 to 2013. I created a pivot table and a simple line graph visualization that is saved on a different sheet in the spreadsheet attached.

From the data I filtered and visualized it looked like there was a decrease of DUIs from 2010 (year Uber started in SF) to 2013 from 214 to 180. There was an increase of adult kidnappings from 23 to 49 during that same time period. That time frame also saw a reduction in traffic tickets from 1153 to 281.

To make some sense of this, I did a few binomial tests to check the statistical significance of these changes. This [DMV archive on outstanding Driver's Licenses](https://www.dmv.ca.gov/portal/wcm/connect/90a04dc3-ac0d-4528-a6a3-4797d0842689/dl_outs_by_county.pdf?MOD=AJPERES) gave me a population of 559430 drivers in SF in 2013. Doing a percent decrease of SF's population from 2013 to 2010 (841270 to 805770 = -4.2% so we can estimate there were 535934 drivers in SF in 2010. (.042 * 559430 = ~23496. 559430 - 23496 = 535934).

In this example population (n) would be 559430, 180 is the number of DUI's in 2013 and p = (214/535934 or .0003993028)
`from scipy.stats import binom_test`
`pval = binom_test(180, n=559430, p=.0003993028)
print(pval)`
this pvalue came out to about .003 which means the difference is statistically signficant by most metrics.
It looks like there also was a drop in traffic tickets from 2010 to 2013. I did a binomial test on those metrics with the same populations as well. The p in this case would be the 2010 tickets divided by the 2010 driving population (1153/535934)
`pval2 = binom_test(281, n=559430, p=.0021513843)
print(pval2)`
This pvalue was ~ 2.355706786840076e-225 which is also statistically significant. I would assess that, based on the data, there is a noticable drop in DUI's in San Francisco after the introduction of Uber.
