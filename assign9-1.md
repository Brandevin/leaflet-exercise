Population distribution in US with leaflet

=============
Name: Brandevin
Date:01/01/2021

A plot with the 1000 most populated cities in the us is made
Data extracted from: https://simplemaps.com/data/us-cities


```r
library(dplyr)
library(leaflet)

data<-read.csv('uscities.csv',sep=',')[c('city','lat','lng','population')]

top_pop<- data %>% top_n(1000)
```

```
## Selecting by population
```

```r
label<- paste(paste('City: ',top_pop$city,' - Population:', as.character(format(as.numeric(top_pop$population),nsmall=0,big.mark=','))))
m<-top_pop %>%
                leaflet() %>%
                addTiles(urlTemplate = 'http://{s}.tile.opentopomap.org/{z}/{x}/{y}.png') %>%
               addCircleMarkers(~lng,~lat,popup=~as.character(city),label=label,radius=sqrt(top_pop$population)/200)%>%
                addProviderTiles(providers$CartoDB.Positron)  

library(htmlwidgets)
saveWidget(m, file="m.html")
```


```r
knitr::include_url("m.html", height="1080px")
```

```
## Could not load  file:///C:/Users/felip/AppData/Local/Temp/RtmpKi8bW2/file4ffc1f0f1a9e/m.html
```

```
## Error in (function (url = NULL, file = "webshot.png", vwidth = 992, vheight = 744, : webshot.js returned failure value: 1
```
