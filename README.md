The following exercises are a test in disguise.

What do you think about the coding?

Can you think of any improvements to the following?

install.packages("tidyverse") #uncomment to install tidyverse if you haven't already

```{r}
library(tidyverse)
```

## PROBLEM 1

> visualizing your data is important! summary statistics can be highly misleading, and simply plotting the data can reveal a lot more! Lets look at the Anscombe's Quartet data. There are four different data sets. Anscombe, F. J. (1973). "Graphs in Statistical Analysis". American Statistician. 27 (1): 17--21. <doi:10.1080/00031305.1973.10478966>. JSTOR 2682899.

```{r}
anscombe_quartet = readRDS("../dataset/anscombe_quartet.rds")
```

### Let's explore the dataset

```{r}
str(anscombe_quartet)
```

### What does the function str() do?

it provides a summary of the structure of the dataset, including the type of object, the number of elements it contains, and the structure of its elements.

### Let's check some summary statistics:

```{r}
anscombe_quartet %>% 
  group_by(dataset) %>% 
  summarise(
    mean_x    = mean(x),
    mean_y    = mean(y),
    min_x     = min(x),
    min_y     = min(y),
    max_x     = max(x),
    max_y     = max(y),
    crrltn    = cor(x, y)
  )
```

### What do the summary statistics tell us about the different datasets?

### Let's plot the data with ggplot:

```{r}
require(ggplot2)

 ggplot(anscombe_quartet, aes(x=x,y=y)) +
  geom_point() + 
  geom_smooth(method = "lm",formula = "y ~ x") +
  facet_wrap(~dataset)
```

### Save the plot

```{r}
ggsave("../plot/anscombe_quartet.png", width = 20, height = 20, units = "cm")
```

![anscombe_quartet](plot/anscombe_quartet.png)

### What do the plots tell us about the different datasets?

not all datasets fit the linear regression model \# describe the relationship between x and y in the different datasets.

### Would linear regression be an appropriate statistical model to analyse the x-y relationship in each dataset?

no \# what conclusions can you draw for the plots and summary statistics? even if the data itself is not linear correlated but there still might be a linear mode generated.

## PROBLEM 2

### Load in the datasaurus dataset

```{r}
datasaurus_dozen = readRDS("../dataset/datasaurus_dozen.rds")
```

### Explore the dataset

```{r}
datasaurus_dozen %>%
  group_by(dataset) %>%
  count()

datasaurus_dozen %>% 
  group_by(dataset) %>% 
  summarise(
    mean_x    = mean(x),
    mean_y    = mean(y),
    min_x     = min(x),
    min_y     = min(y),
    max_x     = max(x),
    max_y     = max(y)
  )
```

### How many rows and columns does the datasaurus_dozen file have?

1846 3

```{r}
ggplot(datasaurus_dozen, aes(x=x,y=y)) +
  geom_point() + 
  facet_wrap(~dataset)
```

### Calculate the correlations and summary statistics for x and y in all datasets:

```{r}
datasaurus_dozen %>%
  group_by(dataset) %>%
  summarise(
    crrltn = cor(x, y))
```

### Plot the relationships between x and y in each dataset including the line of best fit.

```{r}
ggplot(datasaurus_dozen, aes(x=x,y=y)) +
  geom_point() + 
  geom_smooth(method = "lm",formula = "y ~ x") +
  facet_wrap(~dataset)
```

### Save the plot

```{r}
ggsave("../plot/datasaurus_dozen.png", width = 20, height = 20, units = "cm")

```

![datasaurus_dozen](plot/datasaurus_dozen.png)

### What conclusions can you draw for the plots and summary statistics?

lm may not be the best model to use for these datasets
