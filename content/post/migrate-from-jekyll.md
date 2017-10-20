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

<pre class="r"><code>query&lt;-&quot;SELECT playerID,sum(HR),sum(SO)
FROM Batting 
GROUP BY playerID
HAVING sum(HR)&gt;400&quot;
sqldf(query)</code></pre>
<pre><code>##     playerID sum(HR) sum(SO)
## 1  aaronha01     755    1383
## 2  bagweje01     449    1558
## 3  bankser01     512    1236
## 4  beltrad01     445    1584
## 5  beltrca01     421    1693
## 6  bondsba01     762    1539
## 7  cabremi01     446    1516
## 8  cansejo01     462    1942
## 9  dawsoan01     438    1509
## 10 delgaca01     473    1745
## 11  dunnad01     462    2379
## 12 evansda01     414    1410
## 13  foxxji01     534    1311
## 14 gehrilo01     493     790
## 15 giambja01     440    1572
## 16 gonzaju03     434    1273
## 17 griffke02     630    1779
## 18 guerrvl01     449     985
## 19 jacksre01     563    2597
## 20 jonesan01     434    1748
## 21 jonesch06     468    1409
## 22 killeha01     573    1699
## 23 kingmda01     442    1816
## 24 konerpa01     439    1391
## 25 mantlmi01     536    1710
## 26 matheed01     512    1487
## 27  mayswi01     660    1526
## 28 mccovwi01     521    1550
## 29 mcgrifr01     493    1882
## 30 mcgwima01     583    1596
## 31 murraed02     504    1516
## 32 musiast01     475     696
## 33 ortizda01     541    1750
## 34   ottme01     511     896
## 35 palmera01     569    1348
## 36 piazzmi01     427    1113
## 37 pujolal01     591    1053
## 38 ramirma02     555    1813
## 39 ripkeca01     431    1305
## 40 robinfr02     586    1532
## 41 rodrial01     696    2287
## 42  ruthba01     714    1330
## 43 schmimi01     548    1883
## 44 sheffga01     509    1171
## 45 snidedu01     407    1237
## 46 soriaal01     412    1803
## 47  sosasa01     609    2306
## 48 stargwi01     475    1936
## 49 teixema01     409    1441
## 50 thomafr04     521    1397
## 51 thomeji01     612    2548
## 52 willibi01     426    1046
## 53 willite01     521     709
## 54 winfida01     465    1686
## 55 yastrca01     452    1393</code></pre>


... Then we need to save this data in result ...

<pre class="r"><code>query&lt;-&quot;SELECT playerID,sum(HR),sum(SO)
FROM Batting 
GROUP BY playerID
HAVING sum(HR)&gt;400&quot;
results<-sqldf(query)</code></pre>

... now to visulaize the data ...

<pre class="r"><code>ggplot()+
  geom_point(data=result,aes(x=career_SO,y=career_HR),size=3, color="blue")+
  ggtitle("Career Strikeouts VS Homeruns For Great Hitters")+
  xlab("career Strikeouts")+
  ylab("Career Homeruns")</code></pre>
  
