## 2020 Presidential Election Blog
# Gov1347: Election Analytics

```{r included = FALSE}
library(tidyverse)
library(ggplot2)
library(usmap)

popvote_df <- read_csv("popvote_1948-2016.csv")
```
Did this work?

```{r include = FALSE}
## subset
popvote_df %>% 
  filter(year == 2016) %>% 
  select(party, candidate, pv2p)

## format
(popvote_wide_df <- popvote_df %>%
  select(year, party, pv2p) %>%
  spread(party, pv2p))

## modify
(popvote_wide_df <- popvote_wide_df %>% 
  mutate(winner = case_when(democrat > republican ~ "D",
                            TRUE ~ "R")))

## summarise
popvote_wide_df %>% 
  group_by(winner) %>%
  summarise(races = n())
```
Now lets try a plot

```{r}
ggplot(popvote_df, aes(x = pv2p)) + 
    geom_histogram()
```