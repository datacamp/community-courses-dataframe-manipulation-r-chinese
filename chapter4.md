---
title_meta  : 第四章
title       : 欄位聚合數值的計算
description : 分析資料框常需要對某些欄位進行摘要統計，可能是求取總和或者平均值，讓你對變數的分佈更為清楚；有時候甚至你需要依據某個類別變數，分別計算不同類別的摘要統計，一如你在 Excel 中使用樞紐分析表一般。我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:eb29a9a1a9
## 摘要統計

你與草帽海賊團同樣屬於**超新星世代**，知己知彼，百戰不殆。你打算要針對這個潛在對手好好分析，在第一章中我們曾經有介紹過 [summary()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/summary) 函數，它可以幫助你快速暸解資料框的摘要，而[summary()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/summary) 函數除了可以應用在整個資料框之外，其實也可以使用在單一的變數上：

```{r}
summary(df$col)
```

我們也可以善用簡單的 [sum()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/sum) 函數或 [sd()](http://www.rdocumentation.org/packages/stats/versions/3.3.1/topics/sd) 函數產出統計值，不一定只能仰賴 [summary()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/summary) 函數產出既定的摘要統計值。

*** =instructions
- 對草帽海賊團資料框使用 `summary()` 函數
- 對草帽海賊團資料框之中的 `height` 變數使用 `summary()` 函數
- 對草帽海賊團資料框之中的 `bounty` 變數使用 `sum()` 函數
- 對草帽海賊團資料框之中的 `bounty` 變數使用 `sd()` 函數

*** =hint
- 將 `straw_hat_df` 作為 `summary()` 函數的唯一參數。
- 將 `straw_hat_df$height` 作為 `summary()` 函數的唯一參數。
- 將 `straw_hat_df$bounty` 作為 `sum()` 函數的唯一參數。
- 將 `straw_hat_df$bounty` 作為 `sd()` 函數的唯一參數。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 已預先載入

# 對 straw_hat_df 使用 summary()


# 對 straw_hat_df$height 使用 summary()


# 對 straw_hat_df$bounty 使用 sum()


# 對 straw_hat_df$bounty 使用 sd()


```


*** =solution
```{r}
# straw_hat_df 已預先載入

# 對 straw_hat_df 使用 summary()
summary(straw_hat_df)

# 對 straw_hat_df$height 使用 summary()
summary(straw_hat_df$height)

# 對 straw_hat_df$bounty 使用 sum()
sum(straw_hat_df$bounty)

# 對 straw_hat_df$bounty 使用 sd()
sd(straw_hat_df$bounty)

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23565; `straw_hat_df` &#20351;&#29992; `summary()` &#20989;&#25976;&#65311;"
test_output_contains("summary(straw_hat_df)",
                     times = 1,
                     incorrect_msg = msg)
                     
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23565; `straw_hat_df$height` &#20351;&#29992; `summary()` &#20989;&#25976;&#65311;"
test_output_contains("summary(straw_hat_df$height)",
                     times = 1,
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23565; `straw_hat_df$bounty` &#20351;&#29992; `sum()` &#20989;&#25976;&#65311;"
test_output_contains("sum(straw_hat_df$bounty)",
                     times = 1,
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23565; `straw_hat_df$bounty` &#20351;&#29992; `sd()` &#20989;&#25976;&#65311;"
test_output_contains("sd(straw_hat_df$bounty)",
                     times = 1,
                     incorrect_msg = msg)

sucess_msg("&#30475;&#21040;&#33609;&#24125;&#28023;&#36042;&#22296;&#20840;&#22296;&#30340;&#25080;&#36062;&#37329;&#38989;&#36889;&#40636;&#39640;&#65292;&#20320;&#26377;&#27794;&#26377;&#35258;&#24471;&#36996;&#26159;&#19981;&#35201;&#25307;&#24825;&#20182;&#20497;&#22909;&#20102;&#21602;&#65311;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:077f2d637a
## 摘要統計（2）

身為**超新星世代**的一員，你對草帽海賊團的戰力分析絕對不僅止於世界政府那粗糙的整體摘要統計，你想著也許針對不同性別或者不同戰鬥位置的船員分開剖析，可以幫助你找到草帽海賊團的弱點，便於在將來正面對決時能加以利用。

於是我們要來學習使用類似在 Excel 中常用的**樞紐分析表**來達成這件事情，為了簡單地做到這件事情，接下來我們要使用 [ddply()](http://www.rdocumentation.org/packages/plyr/versions/1.8.4/topics/ddply) 函數，跟我們先前使用的函數不一樣的地方在於，它不是 R 語言的原生函數，而是源自於一個套件 [plyr](http://www.rdocumentation.org/packages/plyr/versions/1.8.4)，因此在使用之前必須要使用 [library()](http://www.rdocumentation.org/packages/SIM/versions/1.42.0/topics/Library) 函數將 [plyr](http://www.rdocumentation.org/packages/plyr/versions/1.8.4) 套件載入才行。

```{r}
library(plyr)
```

