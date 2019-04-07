---
authors:
- admin
date: "2018-11-30T00:00:00-04:00"
lastmod: "2018-11-30T00:00:00-04:00"
draft: false
image:
  focal_point: "Smart"
  preview_only: false
subtitle: 'A quick demographic study of veterans across the United States and New York.'
summary: Drawing insights on population through data visualization.
title: 'Visualizing Veteran Population'
categories: ["Data Visualization", "GIS"]
reading_time: true
---

The [US Department of Veterans Affairs](https://www.va.gov/) is a federal agency responsible for taking care of US military personnel after they separated from service. The VA provides healthcare, education, disability, and other benefits to US veterans. The [VA](https://www.va.gov/vetdata/veteran_population.asp) also has a lot of data on US veterans available for free. There's a bunch of spreadsheets and pivot tables on veteran population. The data is given in county format, which is good for our analysis later, but we need to aggregate the data to view it at a state level.

## <b>US Veteran Population Density in 2015</b>
![png](./gallery/uspop.png)
Here is a breakdown of veteran population density across the US in 2015. We can see that most veterans live in California, Texas, and Florida.

<br>
## <b>New York Veteran Population Density in 2015</b>
![png](./gallery/nypopraw.png)
Now that we have an idea of the veteran population in the US, let's look more closely at a particular state to see if we can draw any insights on this dataset. The above map shows a raw count of veterans in New York. Suffolk County and Erie County have the most veterans. However, this map can be a little misleading. There are a lot of veterans living in these counties but we do not know anything about the overall population density in each county. Let's take some [census data](https://www.census.gov/programs-surveys/geography.html) and build out veteran proportion in each country.

<br>
## <b>New York Veteran Population by percentage</b>
![png](./gallery/nypopperc.png)
Now we can see that Jefferson and Hamilton County have the most veterans by percentage of population within the county. A little Google search found that there's a VA in both Hamilton County and Jefferson County!
<br>
[VA in Hamilton County](https://veterans.ny.gov/content/hamilton-county-veterans-service-agency-location-1)<br>
[VA in Jefferson County](https://co.jefferson.ny.us/departments/Veterans)

<br>

## <b>Importance of Visualization</b>
Visualizing this dataset helped us understand that areas with the highest proportion of veterans do not happen by chance. More veterans will live nearby a VA.  I think this approach would be useful for the VA if they have plans to build new VA hospitals or offices that provide benefits to veterans.

<br>
### Resources:  
https://www.census.gov/geo/maps-data/data/cbf/cbf_state.html  
http://gis.ny.gov/gisdata/inventories/details.cfm?DSID=927  
https://www.va.gov/vetdata/