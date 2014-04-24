Getting-Cleaning-Data-Quiz3
===========================
Question 1
The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv 

and load the data into R. The code book, describing the variable names is here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FPUMSDataDict06.pdf 

Create a logical vector that identifies the households on greater than 10 acres who sold more than $10,000 worth of agriculture products. Assign that logical vector to the variable agricultureLogical. Apply the which() function like this to identify the rows of the data frame where the logical vector is TRUE. which(agricultureLogical) What are the first 3 values that result?

Your Answer		Score	Explanation
403, 756, 798			
236, 238, 262			
59, 460, 474			
125, 238,262	Correct	3.00

```{r}
setwd("C:/Users/Music/Desktop/R/Coursera - Getting and Cleaning Data/Quiz 3/")
tempFile <- tempfile()
filePath  <- file.path(getwd())
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv",tempFile, mode = 'wb') 

q1Df <- read.csv(tempFile)
file.remove(tempFile) 

q1Df$agricultureLogical = ifelse(q1Df$ACR==3 & q1Df$AGS==6, TRUE, FALSE)
which(q1Df$agricultureLogical)
```
Question 2
Using the jpeg package read in the following picture of your instructor into R 

https://d396qusza40orc.cloudfront.net/getdata%2Fjeff.jpg 

Use the parameter native=TRUE. What are the 30th and 80th quantiles of the resulting data?
Your Answer		Score	Explanation
-10904118 -10575416			
-15259150 -594524			
-16776430 -15390165			
-15259150 -10575416	Correct	3.00

```{r}
library(jpeg)

tempFile <- tempfile()
filePath  <- file.path(getwd())
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fjeff.jpg" ,tempFile, mode = 'wb') 

jpeg <- readJPEG(tempFile, native = TRUE)
file.remove(tempFile)

quantile(jpeg, probs = c(.3,.8))
```
Question 3
Load the Gross Domestic Product data for the 190 ranked countries in this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv 

Load the educational data from this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv 

Match the data based on the country shortcode. How many of the IDs match? Sort the data frame in descending order by GDP rank. What is the 13th country in the resulting data frame? 

Original data sources: 
http://data.worldbank.org/data-catalog/GDP-ranking-table 
http://data.worldbank.org/data-catalog/ed-stats
Your Answer		Score	Explanation
234, St. Kitts and Nevis			
189, St. Kitts and Nevis	Correct	3.00	
234, Spain			
190, Spain			
190, St. Kitts and Nevis			
189, Spain
```{r}
tempFile <- tempfile()
filePath  <- file.path(getwd())
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv",tempFile, mode = 'wb') 

GDPDf <- read.csv(tempFile)
file.remove(tempFile) 

tempFile <- tempfile()
filePath  <- file.path(getwd())
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv",tempFile, mode = 'wb') 

edDf <- read.csv(tempFile)
file.remove(tempFile) 

length(which(GDPDf2[,1] %in% edDf[,1]))

GDPDf2=GDPDf[5:330,c(1:2,4)]
GDPDf3=GDPDf2[1:190,]
GDPDf3[,2]=as.character(GDPDf3[,2])   # convert from factor to char
GDPDf3[,2]=as.numeric(GDPDf3[,2])     # convert from char to num
GDPDf3[order(GDPDf3$GDPRank, decreasing = TRUE),][13,]
```
Question 4
What is the average GDP ranking for the "High income: OECD" and "High income: nonOECD" group?
Your Answer		Score	Explanation
30, 37			
23.966667, 30.91304			
23, 45			
133.72973, 32.96667			
32.96667, 91.91304	Correct	3.00	
23, 30
```{r}
