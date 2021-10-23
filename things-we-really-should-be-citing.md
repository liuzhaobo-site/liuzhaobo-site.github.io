---
title: "We Should Really Be Citing These Things More"
output:
  md_document:
    variant: gfm
    preserve_yaml: TRUE
    pandoc_args: 
      - "--wrap=preserve"
author: "steve"
excerpt: "Use some R code (and SQL code) to create dyadic dispute-year data from participant-level summaries."
layout: page
categories:
  - R
  - Political Science
# image: "putin-visit-denmark-2011.jpg"
---

This page will serve as a bibliography/running tally of things that we (certainly I) use a lot in our applied research, but we almost never cite these things as integral to the output submitted for peer review. Here’s the problem as I see it.

1.  The need to do more runs head-first into the stringent space restrictions of our journals. This creates a tension where the tools we use collide with our publication outlets that simultaneously expect us to do more without any increase in the journal’s capacity to allow us to communicate more.
2.  The tools themselves are both integral to our workflow, but only indirectly related—at most—to the material. For example, there were no doubt dozens—maybe over 100—peace science articles published in the mid-2000s that used EUGene for constructing the data. The analysis may have been one of several at the time seeking to explain variation in inter-state conflict by reference to democracy. [Jones et al. (1996)](https://journals.sagepub.com/doi/10.1177/073889429601500203) or [Ghosn et al. (2004)](https://journals.sagepub.com/doi/10.1080/07388940490463861?icid=int.sj-abstract.similar-articles.2) may have been appropriately cited for the conflict data. The user may have also cited a given [Polity](https://www.systemicpeace.org/inscrdata.html) user manual for the democracy data. In all likelihood, they omitted that software introduced by [Bennett and Stam (2000)](https://www.tandfonline.com/doi/abs/10.1080/03050620008434965) created the data for them.[^1] Something has to be omitted for space, and it’s likely going to be the ancillary stuff.[^2]  
3.  Relative to the period when I started my path in academia, I think we have a glut of researchers producing more public goods than ever before. There’s a wealth of information out there regarding various computational methods, various parlor tricks for reproducible research, or various other tools that expedite our research processes. We’re all better off for it, and we should all appreciate it.
4.  However, there aren’t too many incentives for people in academia who provide these goods. Their contributions are rarely cited and journals in the discipline don’t typically advertise space or interest in these public goods. To be clear, there are publication outlets available—prominently [*Journal of Open Source Software*](https://joss.theoj.org)—but I highly doubt I’m the first person who has been told by more senior people or administrators that these outlets are considered “less than” other more “prestigious”, discipline-specific outlets.

What I pledge and offer here can’t address all these issues. That said, my experience has shown that administrators increasingly prioritize scholarly indicators of “impact” in doing end-of-year evaluations for performance and the sporadic “merit” reviews for raises. Increasingly, that’s [Google Scholar](https://scholar.google.com). If journals don’t permit space for us to cite all the important ancillary stuff, we can at least 1) stick those citations in an appendix, 2) put the appendix online at our website, 3) wait for Google to crawl our site to find those citations, and 4) let those register on people’s Google Scholar profiles to count toward their [*h*-index](https://guides.lib.umich.edu/c.php?g=282982&p=1887449) and [*i*10-index](https://ucsd.libguides.com/c.php?g=704382&p=5000890#:~:text=i10-Index%20=%20the%20number%20of,Advantages%20of%20i10-Index). It’ll at least be what I pledge to do going forward.

## Stuff I Use a Lot in My Research

What follows is an incomplete and expanding list of tools I use in all/most of my research projects. I may not use all of them in a given project (i.e. if I’m doing something Bayesian, I’m not going to be doing something with clustered standard errors). No matter, I use these a lot—you probably do too—and we should all cite them more.

``` r
library(tidyverse)
library(bib2df)
library(stevemisc)

things_to_cite <- bib2df("~/Dropbox/svmiller.github.io/miscelanea/things-you-should-cite.bib")

print_refs(capture.output(df2bib(things_to_cite)), toformat='plain')
```

Arel-Bundock, Vincent. 2021a. Modelsummary: Summary Tables and Plots for
Statistical Models and Data:
<https://CRAN.R-project.org/package=modelsummary>.

———. 2021b. WDI: World Development Indicators and Other World Bank Data.
<https://CRAN.R-project.org/package=WDI>.

Arel-Bundock, Vincent, Nils Enevoldsen, and CJ Yetman. 2018.
“Countrycode: An R Package to Convert Country Names and Country Codes.”
Journal of Open Source Software 3(28): 848.
<https://doi.org/10.21105/joss.00848>.

Bates, Douglas, Martin Mächler, Ben Bolker, and Steve Walker. 2015.
“Fitting Linear Mixed-Effects Models Using lme4.” Journal of Statistical
Software 67(1): 1–48.

Bergé, Laurent. 2018. “Efficient Estimation of Maximum Likelihood Models
with Multiple Fixed-Effects: The R Package FENmlm.” CREA Discussion
Papers (13).

Bürkner, Paul-Christian. 2017. “Brms: An R Package for Bayesian
Multilevel Models Using Stan.” Journal of Statistical Software 80(1):
1–28.

———. 2018. “Advanced Bayesian Multilevel Modeling with the R Package
brms.” The R Journal 10(1): 395–411.

Chung, Yeojin et al. 2013. “A Nondegenerate Penalized Likelihood
Estimator for Variance Parameters in Multilevel Models.” Psychometrika
78(4): 685–709.

Xie, Yihui. 2015. Dynamic Documents with R and Knitr. Chapman; Hall/CRC.

### .bib Entries

Here are the .bib entries if you’d like to add them to your own file.

``` r
df2bib(things_to_cite)
#> @Article{arelbundocketal2018c,
#>   Author = {Vincent Arel-Bundock and Nils Enevoldsen and CJ Yetman},
#>   Journal = {Journal of Open Source Software},
#>   Number = {28},
#>   Pages = {848},
#>   Title = {countrycode: An {R} package to convert country names and country codes},
#>   Volume = {3},
#>   Year = {2018},
#>   Url = {https://doi.org/10.21105/joss.00848}
#> }
#> 
#> 
#> @Book{xie2015ddrk,
#>   Author = {Yihui Xie},
#>   Publisher = {Chapman and Hall/CRC},
#>   Title = {Dynamic Documents with {R} and knitr},
#>   Year = {2015}
#> }
#> 
#> 
#> @Manual{arelbundock2021m,
#>   Author = {Vincent Arel-Bundock},
#>   Note = {R package version 0.9.2},
#>   Title = {modelsummary: Summary Tables and Plots for Statistical Models and Data:},
#>   Year = {2021},
#>   Url = {https://CRAN.R-project.org/package=modelsummary}
#> }
#> 
#> 
#> @Manual{arelbundock2021w,
#>   Author = {Vincent Arel-Bundock},
#>   Note = {R package version 2.7.4},
#>   Title = {WDI: World Development Indicators and Other World Bank Data},
#>   Year = {2021},
#>   Url = {https://CRAN.R-project.org/package=WDI}
#> }
#> 
#> 
#> @Article{berge2018eeml,
#>   Author = {Laurent Berg\'e},
#>   Journal = {CREA Discussion Papers},
#>   Number = {13},
#>   Title = {Efficient estimation of maximum likelihood models with multiple fixed-effects: the {R} package {FENmlm}},
#>   Year = {2018}
#> }
#> 
#> 
#> @Article{batesetal2015flmm,
#>   Author = {Douglas Bates and Martin M{\"a}chler and Ben Bolker and Steve Walker},
#>   Journal = {Journal of Statistical Software},
#>   Number = {1},
#>   Pages = {1--48},
#>   Title = {Fitting Linear Mixed-Effects Models Using {lme4}},
#>   Volume = {67},
#>   Year = {2015},
#>   Doi = {10.18637/jss.v067.i01}
#> }
#> 
#> 
#> @Article{chungetal2013ndpl,
#>   Author = {Chung, Yeojin and Sophia Rabe-Hesketh and Vincent Dorie and Andrew Gelman and Jingchen Liu},
#>   Journal = {Psychometrika},
#>   Number = {4},
#>   Pages = {685--709},
#>   Title = {A Nondegenerate Penalized Likelihood Estimator for Variance Parameters in Multilevel Models},
#>   Volume = {78},
#>   Year = {2013},
#>   Owner = {steve},
#>   Timestamp = {2015.07.21}
#> }
#> 
#> 
#> @Article{burkner2018abmm,
#>   Author = {Paul-Christian B{\"u}rkner},
#>   Journal = {The R Journal},
#>   Number = {1},
#>   Pages = {395--411},
#>   Title = {Advanced {Bayesian} Multilevel Modeling with the {R} Package {brms}},
#>   Volume = {10},
#>   Year = {2018},
#>   Doi = {10.32614/RJ-2018-017},
#>   Encoding = {UTF-8}
#> }
#> 
#> 
#> @Article{burkern2017brms,
#>   Author = {Paul-Christian B{\"u}rkner},
#>   Journal = {Journal of Statistical Software},
#>   Number = {1},
#>   Pages = {1--28},
#>   Title = {brms: An {R} Package for {Bayesian} Multilevel Models Using {Stan}},
#>   Volume = {80},
#>   Year = {2017},
#>   Doi = {10.18637/jss.v080.i01},
#>   Encoding = {UTF-8}
#> }
```

[^1]: The researcher borrows trouble when they do this because software like EUGene implements its own design choices on the construction of the data that are almost never communicated to the reader. They may even be unaware to the researcher.

[^2]: Let he who is without sin cast the first stone; my [first](https://journals.sagepub.com/doi/abs/10.1177/0738894211404797) [two](https://journals.sagepub.com/doi/full/10.1177/0022002712446126) publications are guilty of this.
