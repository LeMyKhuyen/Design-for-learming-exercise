# Design-for-learming-exercise
ggplot2 tutorial 1


coding for Rstudio
---
title: "ggplot2 Tutorial"
output: learnr::tutorial
runtime: shiny_prerendered
progressive: true
allow_skip: true
---

```{r setup, include=FALSE}
library(learnr)
library(tidyverse)
knitr::opts_chunk$set(echo = FALSE)
# setup everything that exercise chunks need to know about here
load('data/course1_data.rda')
dat <- select(dat, -Grade_Category) # drop column with only NAs
dat$final_grade <- round(dat$final_grade, 0)  # Round final grades 
```

## Load data and plot a first graph

The data set sits in the file `course1_data.rda` and once loaded can be accessed in the variable `dat`. The table shows the first 6 rows. Note that you need to page right (click the arrow) to see additional columns. 

```{r}
head(dat)
```

The data consist of 603 rows and 22 columns. Each row contains data on a particular student taking a particular course. We have 26 different courses (`distinct(dat, course_id)`) and 580 students (`distinct(dat, student_id)`). A few students enrolled in more than course.

The variables comprise course and student ID, grade related info, 10 questions from a pre-course survey, and the time in the course as logged by the LMS (in minutes)

### First (scatter) plot

There are many questions one can have on this data set. To get us started, let's look at the relation between time spent on the course is related to final grades. Before we use ggplot2 to display these two variables plotted against each other, think about it for a minute what the relation would be and what it would look like. Sketch on paper!

```{r first_plot, exercise=TRUE, exercise.lines = 7}
dat %>%
  ggplot(aes(x = TimeSpent, y = final_grade)) + 
  geom_point(color = "green")  +
  labs(x = "Time Spent",
    y = "Final Grade")
```

### Exercise with Hint

*Here's an exercise where the chunk is pre-evaluated via the `exercise.eval` option (so the user can see the default output we'd like them to customize). We also add a "hint" to the correct solution via the chunk immediate below labeled `print-limit-hint`.*

Modify the following code to change the color of the plotted points to red:

```{r change-color, exercise=TRUE, exercise.eval=TRUE}
dat %>%
  ggplot(aes(x = TimeSpent, y = final_grade)) + 
  geom_point(color = "green")  +
  labs(x = "Time Spent",
    y = "Final Grade")
```

```{r change-color-hint}
geom_point(color = "red")
```

## Topic 2

Adding a third variable

```{r}
dat %>%
  ggplot(aes(x = TimeSpent, y = final_grade, color = Gender)) + 
  geom_point()  +
  labs(x = "Time Spent",
    y = "Final Grade")
```

### Quiz

*You can include any number of single or multiple choice questions as a quiz. Use the `question` function to define a question and the `quiz` function for grouping multiple questions together.*

Some questions to verify that you understand the purposes of various base and recommended R packages:

```{r quiz}
quiz(
  question("scatter plot show...",
    answer("One categorial varible"),
    answer("Two categorial varibles"),
    answer("Two continuous varibles", correct = TRUE),
    answer("The frequency of values of variables")
  ),
  question("In a scatterplot, an outlier...?",
    answer("...is something we didn't learn 8th grade"),
    answer("...is a point that is far outside the main cluster of points/ordered pairs", correct = TRUE),
    answer("...is a puppet with a long nose named Pinocchio"),
    answer("...is a really naughty point who doesn't tell the truth when outside")
  )
)
```
