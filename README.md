[![Travis-CI Build Status](https://travis-ci.org/reconhub/dibbler.png?branch=master)](https://travis-ci.org/reconhub/dibbler)
[![Build status](https://ci.appveyor.com/api/projects/status/02rb8c5j288gg6vg/branch/master?svg=true)](https://ci.appveyor.com/project/thibautjombart/dibbler/branch/master)
[![codecov](https://codecov.io/gh/reconhub/dibbler/branch/master/graph/badge.svg)](https://codecov.io/gh/reconhub/dibbler)






*dibbler*: investigation of food-borne disease outbreaks
========================================================

> *And then you bit onto them, and learned once again that Cut-me-own-Throat
>   Dibbler could find a use for bits of an animal that the animal didn't know
>   it had got. Dibbler had worked out that with enough fried onions and mustard
>   people would eat anything.* [Terry Pratchett, Moving Pictures.]

*dibbler* provides tools for investigating food-borne outbreaks with (at least
partly) known food distribution networks, and genetic information on the cases.
This document provides an overview of the package's content.


Installing *dibbler*
-------------
To install the development version from github:

```r
library(devtools)
install_github("thibautjombart/dibbler")
```

The stable version can be installed from CRAN using:

```r
install.packages("dibbler")
```

Then, to load the package, use:

```r
library("dibbler")
```

```
## Error in library("dibbler"): there is no package called 'dibbler'
```


A short demo
------------

Here is a short demonstration of the package using an anonymised Salmonella
outbreak dataset, distributed in the *outbreaks* package as
`s_enteritidis_pt59`. The function `make_dibbler` will match the structure of
the network and the case data, and create a `dibbler` object:

```r
names(s_enteritidis_pt59$graph)
```

```
## Error in eval(expr, envir, enclos): object 's_enteritidis_pt59' not found
```

```r
head(s_enteritidis_pt59$graph)
```

```
## Error in head(s_enteritidis_pt59$graph): object 's_enteritidis_pt59' not found
```

```r
dim(s_enteritidis_pt59$graph)
```

```
## Error in eval(expr, envir, enclos): object 's_enteritidis_pt59' not found
```

```r
s_enteritidis_pt59$cluster
```

```
## Error in eval(expr, envir, enclos): object 's_enteritidis_pt59' not found
```

```r
case_data <- with(s_enteritidis_pt59, 
                  data.frame(id = names(cluster), cluster = cluster))
```

```
## Error in with(s_enteritidis_pt59, data.frame(id = names(cluster), cluster = cluster)): object 's_enteritidis_pt59' not found
```

```r
head(case_data)
```

```
## Error in head(case_data): object 'case_data' not found
```

```r
x <- make_dibbler(net = s_enteritidis_pt59$graph, nodes_data = case_data)
```

```
## Error in make_dibbler(net = s_enteritidis_pt59$graph, nodes_data = case_data): could not find function "make_dibbler"
```

```r
x
```

```
## Error in eval(expr, envir, enclos): object 'x' not found
```


The resulting object is an extension of `epicontact` objects; for more
information on these objects, and how to handle them, see the [*epicontacts*
website](http://www.repidemicsconsortium.org/epicontacts/).

Here we plot the object, asking to use `"cluster"` to define colored groups:


```r
plot(x, "cluster")
```

<img src="https://github.com/reconhub/dibbler/raw/master/figs/plot_x.png" width="600px">

This is a screenshot of the actual image, which needs to be visualised on a web broswer.
Groups are indicated in colors, while different types of nodes are indicated with different symbols:

- *entry nodes*: 'origins' of the network, indicated by targets; typically farms

- *internal nodes*: nodes located inside the network, indicated as buildings;
   typically factories or restaurants; note that if the network indicates
   person-to-person transmission, then internal nodes could be cases as well

- *terminal nodes*: nodes located at the periphery of the network, indicated as
   people; typically cases


