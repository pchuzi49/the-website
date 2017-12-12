+++
title = "Visualizing Data"
date = "2017-10-10T13:07:31+02:00"
tags = ["jekyll", "migration", "hugo"]
+++

## Scatter Plots
First it is important to library all the required tools ...

<!--more-->
```{r}
library(Lahman)
library(sqldf)
library(ggplot2)
```

... then it is necessary to extract the data ...

#Extractcing Data----------------------------
```{r}
query<-"SELECT playerID,sum(HR) AS career_HR ,sum(SO) AS career_SO 
FROM Batting
GROUP BY playerID
HAVING sum(HR)>=400"

result<-sqldf(query)

#Visulaizing Data----------------------------

ggplot()+
  geom_point(data=result,aes(x=career_SO,y=career_HR), size=3, color="blue")+
  ggtitle("Career Strikeouts vs. Homeruns for Great Hitters")+
  xlab("Career Strikeouts")+
  ylab("Career Homerunes")
```{r}  
