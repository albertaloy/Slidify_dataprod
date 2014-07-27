---
title       : Weather damage in the United States
subtitle    : 
author      : Albert Aloy
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

</br>

## Abstract

</br>

Weather impact in society is analized by using data records from the U.S. National Oceanic and Atmospheric Administration's (NOAA) storm database.

I report the process of cleaning obtained the data and prepare it in order to show some evidence of which are the weather events that most injuries/fatalities and economic damage produce.

### Libraries used:


```r
library("ggplot2")
library("utils")
library("reshape2")
library("R.utils")
```

--- .class #id

</br>

## Data processing

</br>

The records are obtained from the data from the U.S. National Oceanic and Atmospheric Administration's (NOAA).

Having the <a href="https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2">URL</a> we can proceed to download and unzip to the working directory.


```r
download.file(url,destfile="repdata_data_StormData.csv.bz2", method="curl")
bunzip2("repdata_data_StormData.csv.bz2","repdata_data_StormData.csv",remove=F)
```

And proceed to read it


```r
# Load
data<-read.csv("repdata_data_StormData.csv", stringsAsFactors=FALSE)
```

---

</br>

Having loaded the data, we take the data to the relevant attributes:

- EVTYPE: type of weather event
- FATALITIES: number of fatalities from the event
- INJURIES: number of people injured from the event
- PROPDMG: property damage in dollars
- PROPDMGEXP: property damage exponent (Hundreds, Thousands, Millions, etc.)
- CROPDMG: crop damage in dollars
- CROPDMGEXP: crop damage exponent (Hundreds, Thousands, Millions, etc.)


```r
# Subset
data <- data[c("EVTYPE", "FATALITIES", "INJURIES",
                         "PROPDMG", "PROPDMGEXP", "CROPDMG", "CROPDMGEXP")]
```

---

</br>

Being interested in the variable EVTYPE, which contains the weather events, it'll be useful to set up a vector with common expression patterns to exchange, since the original file is not regulated.


```r
patterns <- c("tstm"="thunderstorm", " \\(.*\\)"="", "^ *"="", "  "=" ", ".*freeze.*"="freeze", 
          ".*freezing.*"="freezing fog", ".*coastal.*"="coastal flood", 
          ".*cold.*"="cold/wind chill", "winter w.*"="winter weather", "mud*"="debris flow",
          ".*surf.*"="high surf", ".*ice.*"="ice storm", ".*frost.*"="frost", 
          "^land.*"="debris flow", ".*debris.*"="debris flow", 
          ".*hurricane.*"="hurricane/typhoon", ".*typhoon.*"="hurricane/typhoon", 
          "^thunderstorm.*"="thunderstorm wind", " [.][0-9]*"="", 
          ".*flash.*flood.*"="flash flood", "lake.*snow.*"="lake-effect snow")
```

</br>

### **To be continued...**

---
