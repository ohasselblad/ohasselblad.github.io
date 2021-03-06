---
layout: default
title: Projects
permalink: projects/
description: A small sample of projects created over the last couple of years.
---

## [](#penn-musa)Geographic Cloud Computing &amp; Visualization

I taught a class in the University of Pennsylvania's Master of Urban Spatial Analytics program. Students built and deployed Flask applications on AWS. Data was stored and processed in a PostgreSQL/PostGIS database on AWS RDS.

See [class GitHub organization](https://github.com/MUSA-509/).

## [](#finding-home)Finding Home

Deciding on where to live in New York City can be a daunting task, so I set out to narrow where my wife and I live by using commute time data between block groups that would have small enough commute times. The goal is to find the block groups in New York where my commute by bike is 30 minutes or less, and my wife's subway + walking commute is 45 minutes or less.

<iframe src="https://eschbacher.carto.com/builder/a7b0fd72-c098-11e6-8a5b-0ef7f98ade21/embed?state=%7B%22map%22%3A%7B%22ne%22%3A%5B40.51448723187888%2C-74.27026988365806%5D%2C%22sw%22%3A%5B40.9533123762605%2C-73.54759937740877%5D%2C%22center%22%3A%5B40.73426159768987%2C-73.90893463053341%5D%2C%22zoom%22%3A10.743441384152003%7D%2C%22widgets%22%3A%7B%223ffe1a69-d539-4a73-8aeb-4b1a9be38692%22%3A%7B%22normalized%22%3Atrue%7D%2C%22113eca2f-dcf0-4b6f-b979-e37bab4061e4%22%3A%7B%22normalized%22%3Atrue%7D%2C%22b40397b1-0823-467f-bbf3-f4d84ae8614b%22%3A%7B%22normalized%22%3Atrue%7D%7D%7D" width="640" height="480"></iframe>


Soon I'll post the Jupyter notebook I wrote to gather the data. The steps are this:

1. Get centroids of all block groups in NYC
2. Get location of place of work for my wife and me
3. Use Google or Mapzen's distance matrix service to get the distance for any block group center to the places of work
    - Use bike commute times for block group to CARTO
    - Use walk + subway commute times for block group to my wife's high school
4. Translate this data into a tabular format using pandas, adding a column of the combined commute times
5. Send to CARTO and make a dashboard

## [](#cartoframes)cartoframes

I wrote v0 of a Python package for integrating CARTO's services into data science workflows. [cartoframes](https://github.com/CartoDB/cartoframes/) allows users to do analysis in Python pandas DataFrames and sync up the DataFrame with a table in CARTO. DataFrames can also be created from a CARTO table, and maps can be made from arbitrary SQL queries against any data in the user database using CartoCSS.


```python
import cartoframes as cf
from cartoframes import Layer
import pandas as pd
cc = cf.CartoContext(api_key='abcdefghijklmnopqrstuvwxyz',
                     base_url='https://eschbacher.carto.com')
df = pd.read_csv('acadia_biodiversity.csv')
cc.write(df, 'acadia_biodiversity')
cc.map(layers=[Layer('acadia_regions'),
               Layer('acadia_biodiversity',
	             color={'column': 'simpson_index'})])
# an embedded interactive map will display
```

See the full project at its GitHub repo: <https://github.com/CartoDB/cartoframes/>.


## Pecan Cookies &emdash; a map thinking engine 

I wrote a 'map thinking engine' that helped CARTO users create new maps by suggesting styles to apply to the map based on properties of the data in the underlying dataset. [TechCrunch](https://techcrunch.com/2015/07/21/cartodb-lets-anyone-visualize-their-data-with-one-click-mapping/) picked up the work, which lives in a [GitHub repo](https://github.com/CartoDB/pecan). I wrote the decision tree and a PoC, and [these stellar developers](https://github.com/CartoDB/pecan/blob/5bdb38443fca6a9e34a3f3a87e778143ef514609/package.json#L24-L29) implemented it within CARTO's Editor and packaging it as a node module.

{% include figure.html caption_text="Draft Pecan Cookies flow chart, eventually implemented in <a href=\"https://github.com/CartoDB/pecan\">CARTO's pecan node module</a>"
                       img_name="pecan-flow-chart.png"
		       alt_text="Draft Pecan Cookies flow chart" %}

The final implementation looked as follows:

{% include figure.html caption_text="Pecan cookies workflow. Image from the blog post <a href=\"\">One-Click Mapping: The Mapping Revolution</a>"
                       img_name="pecan-in-action.png"
		       alt_text="Pecan cookies workflow" %}

## [](#phonetic-teacher)Military Phonetic Alphabet Teacher

My last name is always hard to spell when I'm on the phone with my health insurance company or bank. I struggle to come up with good words for letters ("E as in Edward, S as in uhhh Sam, C as in Cheese, ..."). To make my life easier, I learned the military phonetic alphabet. While just writing the words and letters on some index cards, or using an online resource that does the digitial version, I decided to write a little Python program that allows me to use one of the many great language recongnition services so I can practice speaking instead of just having to type.

The result is in my GitHub account: <https://github.com/andy-esch/phonetic-teacher/>. "Whikey Oscar Whiskey," you'll say!


## [](#andybot)andybot

I made a quick and dirty Slackbot to 'help making some tasks easier at work'. Obviously that didn't happen, but it was fun throwing together a slackbot anyway.

See the project here: <https://github.com/andy-esch/andybot>

## [](#honeymoon-mapping)Honeymoon mapping

My honeymoon took my wife and me from Beijing, China to St. Petersburg, Russia by train. I tracked our GPS location using Moves App, and relied on geotagged images to put the pictures on the map.

I wrote a [blog post](https://carto.com/blog/summer-mapping-project) about it, and wrote some code, in a repo called [img-mapper](https://github.com/andy-esch/img-mapping), that extracts the EXIF data, writes the long/lat (if it exists) to a table along with other information about the image, writes the images to an S3 bucket, sends the table of metadata to CARTO so that the results can be mapped.

 The result is here:

<iframe src="https://team.carto.com/u/eschbacher/viz/3583a1d6-191f-11e5-9190-0e5e07bb5d8a/embed_map" width="640" height="480"></iframe>

## [](#map-academy)Carto(DB)'s Map Academy

I created most of the education content at then CartoDB's [Map Academy](https://carto.com/academy/), which taught CartoDB's Editor and APIs.

The site is all open source: <https://github.com/cartodb/academy>

## [](#cartocamp)CartoCamp

I've been running a meetup to help people learn new skills tangential to making maps and analyzing spatial data. It's called [CartoCamp](https://www.meetup.com/cartocamp/). We were recently listed as one of the [Top 8 Brooklyn meetups](https://technical.ly/brooklyn/2017/07/11/best-technical-meetups/) for learning technology skills.

{% include footer.html %}
