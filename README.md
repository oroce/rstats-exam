### STEP 0.
~~~
data <- read.csv2(file = '/Users/oroce/developing/corvinus/r-stats/list.csv', header=TRUE, sep = ",")
library(rpart)
library(rpart.plot)
data$distance_num <- as.numeric(data$distance)
~~~

### STEP 1.
Most popular departures:
~~~
as.data.frame(rev(sort(table(data$from)))[1:3])
~~~
Result:
~~~
Budapest                              878
Győr                                   68
Vecsés                                 61
~~~

### STEP 2.
Most popular destinations:
~~~
as.data.frame(rev(sort(table(data$to)))[1:3])
~~~
Result:
~~~
Budapest                            919
Győr                                 64
Debrecen                             60
~~~

### STEP 3.
Outliers:
~~~
boxplot(db$distance)
~~~

### STEP 4.
Histogram by hours
~~~
as_date <- as.POSIXlt(data$date, format="%Y-%m-%dT%H:%M:%S")
hist(as_date, "hours")
~~~

### STEP 5.
Are we budapest based?
~~~
prp(rpart(countryside~distance_num,data=data,control=rpart.control(cp=0,maxdepth=3)),type=4,extra=4)
~~~
Very much:
* 70% of all travels are Budapest based
* If users travel more than 92 kms probably they will head to or from Budapest (82%), but if they travel less than 92km there isnt that strong correlation (nly 65% of them are going to or from Budapest)