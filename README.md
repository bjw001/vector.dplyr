---
title: "vector.dplyr User Guide"
author: "Brent Walter"
date: "2016-05-27"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{vector.dplyr User Guide}
  %\VignetteEngine{knitr::rmarkdown}
  \usepackage[utf8]{inputenc}
---

# vectpr.dplyr

vector.dplyr is an R package developed by Rx Solutions that provides Actian Vector backend support for the [dplyr][1] package. It is based on the
vertica.dplyr package developed by Hewlett-Packard. plyr provides tools for data wrangling using R data frames. With vector.dplyr, users can now do the same in Vector tables without moving the data into R. As of the current version the following functionality is available:

* connectivity to Vector via the Ingres JDBC driver
* basic support for queries
* support for Vector date functions such as DATE_TRUNC

Eventually we hope to support easy loading of data into Vector and to take advantage of Vector's parallel load functionality.

For the time being only JDBC connections are supported. And ODBC DSN might or might not work out of the box. JDBC feels like a better interface to 
focus on.

A brief background of the dplyr package is provided in the following section.

### What is dplyr?

*To learn more, read the [dplyr vignette][2].*

dplyr offers convenient methods of manipulating data frames, which can be correlated to tables in a database. Common actions in dplyr include what are known as the "verbs" of the package.

For single data.frames (or tables):

1. **filter**
  * Filters tables by rows matching certain criteria (e.g., filter(table,col1 > 5, col2 ==3)), equivalent to (**SELECT** ... from table **WHERE** ...) 
2. **arrange**
  * Orders rows (for example, arrange(tbl,desc(col1)))
3. **select**
  * Selects columns (for example, select(tbl,'col1','col2'))
4. **mutate**
  * Create new columns (for example, mutate(tbl,new_col1=col3/col2,new_col2=fun(col4,col5)))
5. **summarise** (or **summarize**)
  * Collapses rows belonging to a certain group into a single one (for example, for aggregations)
  * Analogous to **GROUP BY**

There are also verbs for multiple tables, such as left_join(), inner_join(), semi_join(), anti_join(), union(), intersect().

### Actian Vector Integration

For data that resides in a database, dplyr provides an interface to access tables and manipulate them directly inside the database as though they were local data frames. The dplyr package provides support for MySQL, Postgres, BigQuery, and SQLite backends. vector.dplyr enables dplyr to work with Actian Vector.


## Obtaining the Package
You can obtain vector.dplyr from [Github][8].

### Prerequisites
vector.dplyr has 2 hard dependencies: [assertthat](http://cran.r-project.org/web/packages/assertthat/index.html) and [dplyr][1]. There are additional **soft** dependencies on [RJDBC](http://cran.r-project.org/web/packages/RJDBC/index.html)

**Soft** means that there is no enforcement of having these packages installed on the user's system to install vector.dplyr. However, to use vector.dplyr, at least **RJDBC** must be installed and configured. These **soft** dependencies are loaded (at which point it is required to have the package installed) when their specific functionality is invoked. However, vector.dplyr checks to make sure that **RJDBC** is installed and loadable. If it isn't, an error is thrown.

You also need access to an Actian Vector database (must be configured separately), as well as either (or both) the or JDBC Actian Vector driver(s) installed and configured on your host machine (the one that runs vector.dplyr). Please refer to the Vector documentation for help with these steps. The JDBC drivers are available [here](http://esd.actian.com/product/drivers) link.

### Guides, etc.
For now, check out the guide for vertica.dplyr which is [here](https://github.com/vertica/vertica.dplyr)