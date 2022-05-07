---
title: "How Bad America's Gun Violence/Mass Shooting Problem Is, Automated with R Code"
output:
  md_document:
    variant: gfm
    preserve_yaml: TRUE
author: "steve"
date: '2019-08-03'
excerpt: "America's gun violence/mass shooting problem is bad. It's conspicuously bad and it's getting worse despite obvious solutions for which there's no political will."
layout: post
categories:
  - R
  - Political Science
image: "gilroy-strong.jpg"
---





{% include image.html url="/images/gilroy-strong.jpg" caption="Artist Ignacio 'Nacho' Moya carries a sign he made during a vigil for the victims of the Gilroy Garlic Festival Shooting (Nhat V. Meyer/Bay Area News Group)" width=400 align="right" %}

*Last updated:  7 May 2022*

[Another day, another mass shooting](https://www.cnn.com/2019/08/03/us/el-paso-shooting/index.html) for literally the only country of its size and development where this happens on a routine basis. This one in El Paso may (reportedly) have some domestic terrorist overtones to it, but ~~barring confirmation of the shooter and the shooter's motives for the moment~~([nevermind](https://www.nytimes.com/2019/08/03/us/patrick-crusius-el-paso-shooter-manifesto.html)), this post will focus on just the gun violence and the mass shooting angle here.

Gun control emerged as a political and academic hobby horse of mine largely because the problem strikes me as a massive and obvious public health problem that has a fairly simple solution on paper. Cheap gun supply---especially of weapons like AR-15s and AK-47s that have no practical use for hobbyists, hunters, ranchers, or those with an earnest interest in self-defense---decreases the transaction costs associated with carrying out violent rampages (see: [Wintemute, 2005](https://ucdavis.pure.elsevier.com/en/publications/guns-and-gun-violence) and [Bartley and Williams, 2018](https://events.iadb.org/events/handler/geteventdocument.ashx?AFCF784DCD0CBF43BE2C6862BF3344018A6A5CB902FA5578FDC3D0A580A830F93EB421FAAECD73D52562D8C42E362FA5853AE10D3E97D4160C156BD8B16088D305C031362E48EDD5)). The quality of those assault rifles in particular also increases the costs for first-responders, putting them at risk and delaying much needed aid. This raises the societal costs for these "transactions" carried out by perpetrators. Restricting gun supply should raise the transaction costs associated with executing a violent rampage. Again, it's not hard. If you don't believe that, then you don't believe people respond to economic incentives.

Obviously, there's no political will here. [The public opinion is there](http://svmiller.com/research/what-americans-really-think-about-gun-control/) in support of most forms of gun control, even subtly aggressive forms of gun control, but GOP voters are gradually adopting cues from GOP elites on this topic. At the elite-level, the GOP relies on the National Rifle Association---which wants cheap guns for purchase to the benefit of gun manufacturers---to help [message "conservatism" to the voting bloc](https://www.amazon.com/Guns-Democracy-Insurrectionist-Joshua-Horwitz/dp/0472033700) and massage over other issues for GOP partisans (on fiscal policies, for example). The National Rifle Association is well-funded and partisan sorting has made them credible threats to primary GOP legislators who don't cooperate with them.

Alas, here we are: massive public health problem---*needless* public health problem---fairly simple and straightforward policy proposals, and no real (collective) will to do them. 🤷

Anywho, a few lines of R code will emphasize the scope of the problem.

First, [GunPolicy.org](https://www.gunpolicy.org) is an excellent repository of information about gun deaths, gun laws, and gun trafficking for a slew of countries over time. It also has fairly comprehensive coverage of estimated gun homicides per 100,000 people that leans on country reports from various agencies (e.g. Center for Disease Control, United Nations Office on Drugs and Crime, World Health Organization) and incorporates information from academic research on gun homicides as well when necessary. Since we're dealing with advanced countries, there is high confidence in the estimates even if not all years are covered (e.g. the latest year for Germany in the data is 2015).




<!-- United Nations Office on Drugs and Crime data (see: [here](https://www.unodc.org/documents/data-and-analysis/statistics/Homicide/Homicides_by_firearms.xls)) will emphasize how the U.S. stands out among peer countries. I link to the spreadsheet in this post. It's an *ugly* spreadsheet that requires some tidying and eye-balling things in LibreOffice for slicing, but it can be done all the same. Do note: the data are mostly limited to 2009/2010 observations, not that it should meaningfully change the takeaway here. The U.S. will conspicuously be an island among peer countries (i.e. Canada, Australia, New Zealand, and Western/Northern Europe) for its homicide by firearm rate. -->

I gathered data for 25 peer countries to the U.S. (i.e. Western Europe, Northern Europe, Canada, Australia, and New Zealand) in addition to data for the U.S. on gun homicides per 100,000 people in the population. I created a data frame for it (`ghp100k`) and added it to [my `{stevedata}` package.](http://svmiller.com/stevedata). You can [read more about the data here](http://svmiller.com/stevedata/reference/ghp100k.html) and, better yet, [check the underlying sources here](https://www.gunpolicy.org).

We can first assess the scope of the problem by selecting on the latest years for all 25 countres in the data. Here, it's apparent the U.S. will conspicuously be an island among peer countries for its gun homicide rate. The U.S. had a gun homicide rate (per 100,000 people) in 2017 of an astounding 4.46. The next closest country is Canada, with a rate .75. The U.S. rate is almost six times the next closest country in gun homicides.



```r
# require(tidyverse)
# require(stevedata)
# data(ghp100k)

ghp100k %>%
  arrange(country, year) %>%
  group_by(country) %>%
  slice(n()) %>%
  mutate(cy = paste0(country,"\n(", year, ")"),
         cy = fct_lump(cy, value)) %>%
  ggplot(.,aes(cy, value)) +
  theme_steve_web() +
  geom_bar(stat="identity", alpha=0.6, color="black") +
  geom_text(aes(label=round(value, 2)), vjust=-.5, colour="black",
            position=position_dodge(.9), size=4, family="Open Sans") +
  theme(axis.text.x = element_text(angle = 45)) +
  labs(x = "Country (Year)",
       y = "Homicide by Firearm Rate (per 100,000 population)",
       caption = "Data: GunPolicy.org, through various other sources (e.g. UNODC, CDC, WHO).",
       title = "The United States' Gun Homicide Rate (per 100,000 People) is Almost Six Times The Next Closest Peer Country",
       subtitle = "Other countries are reducing what are already low rates. The U.S. rate is only increasing.")
```

![plot of chunk firearm-homicide-rate-data-usa-peer-countries](/images/how-bad-is-americas-gun-violence-mass-shooting-problem-in-a-few-lines-of-r-code/firearm-homicide-rate-data-usa-peer-countries-1.png)

In the event someone may want to copy-paste this information in lieu of showing this graph, you can see the pertinent information here.

<table id="stevetable">
<caption>The Most Recent Homicide by Firearm Rate (per 100,000 People) for the U.S. and Select Peer Countries</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Country </th>
   <th style="text-align:center;"> Year (Most Recent) </th>
   <th style="text-align:center;"> Homicide by Firearm Rate (per 100,000 People) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 4.46 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Canada </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 0.75 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Iceland </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.30 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Italy </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.29 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Sweden </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.26 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Belgium </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.25 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Portugal </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 0.24 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Ireland </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 0.21 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Slovakia </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 0.20 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Greece </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.19 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Australia </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Austria </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Denmark </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Finland </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Luxembourg </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> New Zealand </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Switzerland </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 0.17 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Netherlands </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.16 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> France </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 0.12 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Spain </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.08 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Czechia </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.07 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Germany </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.06 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.06 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Hungary </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 0.05 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> United Kingdom </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 0.02 </td>
  </tr>
</tbody>
</table>

The data I collected have a time-series component as well to assess changes over time. A few things are worth highlighting here. First, data availability isn't as great for the 1990s since GunPolicy.org leans heavily on the Centers for Disease Control to get estimates for homicide rates by firearm. [The Wonder tool](https://wonder.cdc.gov/ucd-icd10.html) has an easy API for data from 1999 to 2017, which would explain why that's the bulk of the data here, in addition to that lonely observation from 1993. Second, the U.S. gun homicide rate had been much worse a few decades ago. This we knew. Crime rates everywhere in the United States were higher a few decades ago than they are now.  Still, the gun homicide rate is *increasing* in the United States since 2009. 

<table id="stevetable">
<caption>The Homicide by Firearm Rate (per 100,000 People) in the United States, 1993 to 2017</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Country </th>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Homicide by Firearm Rate (per 100,000 People) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 1993 </td>
   <td style="text-align:center;"> 7.07 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 3.37 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 1999 </td>
   <td style="text-align:center;"> 3.88 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 3.84 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 3.98 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 4.11 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 4.11 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 3.97 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 4.18 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 4.29 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 4.19 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 4.01 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 3.75 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 3.59 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 3.55 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2012 </td>
   <td style="text-align:center;"> 3.70 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2013 </td>
   <td style="text-align:center;"> 3.55 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 3.45 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 4.04 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 4.46 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> USA </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 4.46 </td>
  </tr>
</tbody>
</table>

By comparison, they're improving in every other country, prominently Italy.


```r

ghp100k %>%
  arrange(country, year) %>%
  ggplot(.,aes(year, value)) + geom_line(size=1.1) +
  theme_steve_web() +
  post_bg() +
  facet_wrap(~country) +
  labs(title = "The Gun Homicide Rate for Select Countries, by Year",
       x = "Year",
       y = "Homicide by Firearm Rate (per 100,000 population)",
       subtitle = "Some countries (Italy, prominently) have done well to address gun violence over time. It's only increased in the U.S. since 2009.",
       caption = "Data: GunPolicy.org, through various other sources (e.g. UNODC, CDC, WHO).")
```

![plot of chunk firearm-homicide-rate-data-usa-peer-countries-yearly-faceted](/images/how-bad-is-americas-gun-violence-mass-shooting-problem-in-a-few-lines-of-r-code/firearm-homicide-rate-data-usa-peer-countries-yearly-faceted-1.png)

Finally, you can start thinking about automating a script to scan [the Mother Jones database on mass shootings](https://www.motherjones.com/politics/2012/12/mass-shootings-mother-jones-full-data/) to note how this problem is only getting worse. In subsequent updates, I might try to fully automate this with built-in assessments of how much worse the problem is getting.

Because it's only getting worse.


```r
library(gsheet)

gsheet2tbl('https://docs.google.com/spreadsheets/d/1b9o6uDO18sLxBqPwl_Gh9bnhW-ev_dABH83M5Vb5L8o/htmlview?sle=true#gid=0') %>%
  separate(date, c("month","day","year"), sep="/") %>%
  mutate(date = lubridate::as_date(paste0(year,"-",month,"-", day))) %>%
  select(case, date, everything()) -> mass_shootings

mass_shootings %>% 
  slice(1) %>%
  select(date) %>% 
  mutate(date = format(date, '%B %d, %Y')) %>% 
  pull(date) -> last_update

mass_shootings %>% 
  slice(1) %>% 
  pull(case) -> most_recent_case

mass_shootings %>% 
  slice(1) %>% 
  pull(location) -> most_recent_location

mass_shootings %>% 
  slice(n()) %>%
  select(date) %>% 
  mutate(date = format(date, '%B %d, %Y')) %>% 
  pull(date) -> first_event

mass_shootings %>%
  mutate(year = lubridate::year(date)) %>%
  group_by(year) %>%
  summarize(n = n()) -> mass_shootings_yearly

mass_shootings_yearly %>%
  filter(year <= 1999) %>%
  summarize(n = sum(n)) %>% pull(n) -> nobs80s90s

mass_shootings_yearly %>%
  filter(year >= 2017) %>%
  summarize(n = sum(n)) %>% pull(n) -> nobssince2017

today <- format(Sys.time(), '%B %e, %Y')

mjms_title = paste0("The Number of Mass Shootings by Year: ", first_event, " Through ", last_update)
mjms_subtitle = paste0("There were ", nobs80s90s, " mass shootings from 1982 to 1999. There have already been ", nobssince2017, " from 2017 through ", last_update,".")
mjms_caption = paste0("Data: Mother Jones. Methodology: mass shootings include at least four deaths from 1982 to Jan. 2013 and include at least three deaths thereafter.\nFigure last updated on ", today, " in the wake of the ", most_recent_case," in ",most_recent_location,".") 

mass_shootings_yearly %>%
  ggplot(.,aes(year, n)) +
  theme_steve_web() +
  geom_bar(stat="identity", alpha=0.4, fill="#619cff",color="black") +
  scale_x_continuous(breaks = seq(1980, 2020, by = 4)) +
  scale_y_continuous(breaks = seq(0, 14, by =2)) +
  geom_text(aes(label=n), vjust=-.5, colour="black",
            position=position_dodge(.9), size=4, family="Open Sans") +
  labs(y = "Number of Mass Shootings in a Calendar Year",
       x = "Year",
       title = mjms_title,
       subtitle =  mjms_subtitle, 
       caption = mjms_caption)
```

![plot of chunk us-mass-shootings-by-year-1982-present](/images/how-bad-is-americas-gun-violence-mass-shooting-problem-in-a-few-lines-of-r-code/us-mass-shootings-by-year-1982-present-1.png)
