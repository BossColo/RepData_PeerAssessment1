# Reproducible Research: Peer Assessment 1

<style>
 th,td{
   padding:2px 5px 2px 5px;
 }
</style>

## Import libraries

```r
require(dtplyr)
require(ggplot2)
require(xtable)
```

## Loading and preprocessing the data
We create data tables grouped by date and by time interval for use later

```r
if (!file.exists('activity.csv')) {
  unzip('activity.zip')
}

activity <- tbl_dt(read.csv('activity.csv', stringsAsFactors=FALSE))
by_date <- activity[, list(total=sum(steps, na.rm=TRUE), 
                           mean=mean(steps, na.rm=TRUE), 
                           median=median(steps, na.rm=TRUE)), 
                    by=date]
by_interval <- activity[, list(mean=mean(steps, na.rm=TRUE)), by=interval]
```

## Histogram of total steps per day

```r
g <- ggplot() + geom_bar(aes(x=as.Date(date, '%Y-%m-%d'), y=total),
                         data=by_date, stat='identity') + 
                labs(x = "Date", y = "Total Steps")

print(g, type='html')
```

![](PA1_template_files/figure-html/histo-1.png)<!-- -->

## What are the mean and median number of steps taken per day?
Median for all days is zero, as zero steps are taken during most intervals

```r
print(xtable(by_date[, list(date, mean, median)]), type='html', include.rownames=FALSE)
```

<!-- html table generated in R 3.3.2 by xtable 1.8-2 package -->
<!-- Thu Jan 26 22:33:51 2017 -->
<table border=1>
<tr> <th> date </th> <th> mean </th> <th> median </th>  </tr>
  <tr> <td> 2012-10-01 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-10-02 </td> <td align="right"> 0.44 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-03 </td> <td align="right"> 39.42 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-04 </td> <td align="right"> 42.07 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-05 </td> <td align="right"> 46.16 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-06 </td> <td align="right"> 53.54 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-07 </td> <td align="right"> 38.25 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-08 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-10-09 </td> <td align="right"> 44.48 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-10 </td> <td align="right"> 34.38 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-11 </td> <td align="right"> 35.78 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-12 </td> <td align="right"> 60.35 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-13 </td> <td align="right"> 43.15 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-14 </td> <td align="right"> 52.42 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-15 </td> <td align="right"> 35.20 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-16 </td> <td align="right"> 52.38 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-17 </td> <td align="right"> 46.71 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-18 </td> <td align="right"> 34.92 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-19 </td> <td align="right"> 41.07 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-20 </td> <td align="right"> 36.09 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-21 </td> <td align="right"> 30.63 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-22 </td> <td align="right"> 46.74 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-23 </td> <td align="right"> 30.97 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-24 </td> <td align="right"> 29.01 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-25 </td> <td align="right"> 8.65 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-26 </td> <td align="right"> 23.53 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-27 </td> <td align="right"> 35.14 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-28 </td> <td align="right"> 39.78 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-29 </td> <td align="right"> 17.42 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-30 </td> <td align="right"> 34.09 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-10-31 </td> <td align="right"> 53.52 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-01 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-11-02 </td> <td align="right"> 36.81 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-03 </td> <td align="right"> 36.70 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-04 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-11-05 </td> <td align="right"> 36.25 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-06 </td> <td align="right"> 28.94 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-07 </td> <td align="right"> 44.73 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-08 </td> <td align="right"> 11.18 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-09 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-11-10 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-11-11 </td> <td align="right"> 43.78 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-12 </td> <td align="right"> 37.38 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-13 </td> <td align="right"> 25.47 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-14 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td> 2012-11-15 </td> <td align="right"> 0.14 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-16 </td> <td align="right"> 18.89 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-17 </td> <td align="right"> 49.79 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-18 </td> <td align="right"> 52.47 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-19 </td> <td align="right"> 30.70 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-20 </td> <td align="right"> 15.53 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-21 </td> <td align="right"> 44.40 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-22 </td> <td align="right"> 70.93 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-23 </td> <td align="right"> 73.59 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-24 </td> <td align="right"> 50.27 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-25 </td> <td align="right"> 41.09 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-26 </td> <td align="right"> 38.76 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-27 </td> <td align="right"> 47.38 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-28 </td> <td align="right"> 35.36 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-29 </td> <td align="right"> 24.47 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td> 2012-11-30 </td> <td align="right">  </td> <td align="right">  </td> </tr>
   </table>

## What is the average daily activity pattern?
Average steps is plotted against daily interval number

Interval minute range can be calculated by (interval number)*5

```r
g <- ggplot(by_interval, aes(x=seq_along(mean), y=mean)) +
                geom_line() +
                labs(x='5 minute interval of day', y='Mean steps taken')

print(g, type='html')
```

![](PA1_template_files/figure-html/inter-1.png)<!-- -->

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
print(by_interval[order(-mean)]$interval[1])
```

```
[1] 835
```

## Imputing missing values
First let's see how many NA's we're working with

```r
print(sum(is.na(activity$steps)))
```

```
[1] 2304
```
The assignment asks for a dataset euqal to the original with the missing data imputed,
but here, I don't believe it to be the best option.

If the missing data was sparse, a linear interpolation between missing points would be a way of
imputing the data. However, it seems that all the NA values appear on days that consist entirely of NA values.
In my opinion, there is no honest way of imputing how many steps would be taken on a day with no data whatsoever.

Here, I think the best option is to remove the missing days from the dataset entirely.

```r
na_days <- by_date$date[is.na(by_date$mean)]
new_activity <- tbl_dt(subset(activity, !(date %in% na_days)))
new_activity$date <- as.Date(new_activity$date, format='%Y-%m-%d')
```

## Are there differences in activity patterns between weekdays and weekends?
First, let's create a new column indicating whether the date of measurement is a weekday or weekend.

```r
new_activity$day <- 
  as.factor(sapply(weekdays(new_activity$date),
         function(x) ifelse(x=='Saturday'|x=='Sunday', 'Weekend', 'Weekday')))
```
Now, we can plot the mean number of steps taken during each 5 minute interval, grouped by weekend or weekday.

```r
g <- ggplot(new_activity[, list(mean=mean(steps)), by=list(day, interval)], aes(x=interval, y=mean)) +
  geom_line() + facet_wrap(~day) + 
  labs(x = "5 minute interval of day", y = "Mean steps taken")

print(g, type='html')
```

![](PA1_template_files/figure-html/plotweekday-1.png)<!-- -->
