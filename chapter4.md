---
title_meta  : 第四章
title       : 欄位聚合與資料轉置
description : 分析資料框常需要對某些欄位進行摘要統計，可能是求取總和或者平均值，讓你對變數的分佈更為清楚；有時候甚至你需要依據某個類別變數，分別計算不同類別的摘要統計，一如你在 Excel 中使用樞紐分析表一般；有經驗的資料科學家還必須熟悉長資料框與寬資料框的互相轉換，視需求靈活調整資料結構。我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

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

[ddply()](http://www.rdocumentation.org/packages/plyr/versions/1.8.4/topics/ddply) 函數需要輸入較多參數，`.variables =` 要放的是欲分別摘要的類別型變數，`.fun = summarise` 在現階段先不做更動，後面則是加上聚合計算欄位的名稱與算式：

```{r}
ddply(df, .variables = c("category1", "category2", ...), .fun = summarise, mean_value1 = mean(value))
```

*** =instructions
- 使用 `head()` 函數看一下草帽海賊團資料框
- 依據性別 `gender` 計算各性別的平均身高
- 依據戰鬥角色 `battle_role` 計算各角色的加總賞金
- 依據性別與戰鬥角色，計算平均身高與加總賞金

*** =hint
- 輸入 `head(straw_hat_df)` 看看資料框
- `.variables = ` 參數要指定為 `"gender"`，聚合計算可以參考 `avg_height = mean(height)`
- `.variables = ` 參數要指定為 `"battle_role"`，聚合計算可以參考 `ttl_bounty = sum(bounty)`
- `.variables = ` 參數要指定為 `c("gender", "battle_role")`，聚合計算可以參考 `avg_height = mean(height), ttl_bounty = sum(bounty)`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
battle_role <- factor(c("戰鬥系", "戰鬥系", "輔助系", "輔助系", "戰鬥系", "輔助系", "輔助系", "戰鬥系", "戰鬥系"))
straw_hat_df$battle_role <- battle_role
```

*** =sample_code
```{r}
# straw_hat_df 已預先載入

# 用 head() 函數看一下 straw_hat_df


# 載入 plyr 套件
library(plyr)

# 依據 gender 計算平均身高
ddply(straw_hat_df, .variables = "__", .fun = summarise, avg_height = mean(__))

# 依據 battle_role 計算加總賞金
ddply(straw_hat_df, .variables = "__", .fun = summarise, ttl_bounty = sum(__))

# 依據 gender 與 battle_role 計算平均身高與加總賞金
ddply(straw_hat_df, .variables = c("__", "__"), .fun = summarise, avg_height = mean(__), ttl_bounty = sum(__))

```

*** =solution
```{r}
# straw_hat_df 已預先載入

# 用 head() 函數看一下 straw_hat_df
head(straw_hat_df)

# 載入 plyr 套件
library(plyr)

# 依據 gender 計算平均身高
ddply(straw_hat_df, .variables = "gender", .fun = summarise, avg_height = mean(height))

# 依據 battle_role 計算加總賞金
ddply(straw_hat_df, .variables = "battle_role", .fun = summarise, ttl_bounty = sum(bounty))

# 依據 gender 與 battle_role 計算平均身高與加總賞金
ddply(straw_hat_df, .variables = c("gender", "battle_role"), .fun = summarise, avg_height = mean(height), ttl_bounty = sum(bounty))

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#20351;&#29992; `head()` &#20989;&#25976;&#30475;&#30475; `straw_hat_df` &#30340;&#21069;&#20845;&#21015;&#65311;"
test_output_contains("head(straw_hat_df)",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `ddply()` &#20989;&#25976;&#20381;&#25818; `gender` &#35336;&#31639;&#21508;&#24615;&#21029;&#30340;&#24179;&#22343;&#36523;&#39640;&#65311;"
test_output_contains("ddply(straw_hat_df, .variables = "gender", .fun = summarise, avg_height = mean(height))",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `ddply()` &#20989;&#25976;&#20381;&#25818; `battle_role` &#35336;&#31639;&#21508;&#25136;&#39717;&#35282;&#33394;&#30340;&#21152;&#32317;&#36062;&#37329;&#65311;"
test_output_contains("ddply(straw_hat_df, .variables = "battle_role", .fun = summarise, ttl_bounty = sum(bounty))",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `ddply()` &#20989;&#25976;&#20381;&#25818; `gender` &#33287; `battle_role` &#35336;&#31639;&#24179;&#22343;&#36523;&#39640;&#33287;&#21152;&#32317;&#36062;&#37329;&#65311;"
test_output_contains("ddply(straw_hat_df, .variables = c("gender", "battle_role"), .fun = summarise, avg_height = mean(height), ttl_bounty = sum(bounty))",
                     incorrect_msg = msg)

success_msg("&#21703;&#65292;&#33021;&#22816;&#23436;&#25104;&#21040;&#36889;&#35041;&#30495;&#30340;&#24456;&#19981;&#31777;&#21934;&#65281;&#26377;&#36889;&#27171;&#30340;&#23526;&#21147;&#25105;&#30456;&#20449;&#20320;&#30495;&#30340;&#26159;&#36229;&#26032;&#26143;&#19990;&#20195;&#30340;&#20854;&#20013;&#19968;&#21729;&#12290;&#25105;&#20497;&#20677;&#20677;&#20171;&#32057;&#20102; `plyr` &#22871;&#20214;&#20013;&#30340;&#19968;&#20491; `ddply()` &#20989;&#25976;&#65292;&#23427;&#35041;&#38957;&#24456;&#26377;&#24456;&#22810;&#20540;&#24471;&#20320;&#33457;&#26178;&#38291;&#21435;&#30740;&#31350;&#30340;&#20989;&#25976;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4
## 資料轉置：寬變長

課程進行到這裡，你的資料整理懸賞金額大概已經由數百元貝里提高到了數百萬貝里，但是要成為一個夠資格與草帽海賊團相抗衡的海賊，你的懸賞金額可得提高到數千萬貝里才行！接下來我們要學習的是關於資料的轉置，學會這個技巧之後可以提升你的資料整理懸賞金額至數千萬貝里！

我們首先介紹如何將一個寬資料框變為長資料框，你記得在草帽海賊團資料框中，我們有 2 個整數欄位嗎？它們分別是 `age` 和 `height`，但你有想過這是我們儲存資料的唯一方法嗎？我們可以改用一個類別欄位儲存數值的種類以及一個數值欄位儲存數值，如此一來不管有多少個數值，我們都可以用兩個欄位儲存！

進行寬資料框變為長資料框時我們需要使用 [gather()](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1/topics/gather) 函數，它不是 R 語言的原生函數，而是源自於一個套件 [tidyr](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1)

*** =instruction
- 載入 `tidyr` 套件。
- 建立一個新的資料框 `straw_hat_wide_df` 僅包含姓名、年齡與身高這三個欄位。

*** =hint
- 使用 `library()` 載入 `tidyr`。
- 可以使用 `[, c("name", "age", "bounty", "height")]` 將欄位選出來。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 已預先載入

# 載入 tidyr 套件


# 建立一個新的資料框 straw_hat_wide_df 僅包含姓名、年齡與身高
straw_hat_wide_df <- 

```

*** =solution
```{r}
# straw_hat_df 已預先載入

# 載入 tidyr 套件
library(tidyr)

# 建立一個新的資料框 straw_hat_wide_df 僅包含姓名、年齡與身高
straw_hat_wide_df <- straw_hat_df[, c("name", "age", "bounty", "height")]

```
*** =sct
```{r}
msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#36617;&#20837; `tidyr` &#22871;&#20214;&#65311;"
test_output_contains("library(tidyr)",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#29986;&#29983; `straw_hat_wide_df` &#20006;&#21253;&#21547;&#22995;&#21517;&#12289;&#24180;&#40801;&#33287;&#36523;&#39640;&#36889;&#19977;&#20491;&#27396;&#20301;&#65311;"
test_object("straw_hat_wide_df",
            undefined_msg = msg, 
            incorrect_msg = msg)

success_msg("&#22909;&#65292;&#29105;&#36523;&#23436;&#30050;&#20102;&#65281;&#25105;&#20497;&#25226;&#36039;&#26009;&#26694;&#31777;&#21270;&#25104;&#19977;&#20491;&#27396;&#20301;&#20043;&#24460;&#35201;&#38283;&#22987;&#20570;&#36681;&#32622;&#22217;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4
## 資料轉置：寬變長（2）

接著我們使用 [gather()](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1/topics/gather) 函數來把寬資料框變為長資料框，[gather()](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1/topics/gather) 函數必須要指定幾個參數，第一個是寬資料框名稱，而 `key = ` 是轉置後用來儲存**數值種類**的欄位名稱，`value = ` 是轉置後用來儲存**數值**的欄位名稱。後面則輸入需要被轉置的原始欄位名稱 :

```{r}
gather(df_wide, key = cate_col, value = num_col, num_col1, num_col2, ...)
```

*** =instruction
- 使用 `gather()` 函數把上一個練習生成的 `straw_hat_wide_df` 轉置為 `straw_hat_long_df`。
- 使用 `head()` 函數看看生成的資料框。

*** =hint
- `gather()` 函數的參數要指派 `straw_hat_wide_df, key = cate, value = int, height, age`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
straw_hat_wide_df <- straw_hat_df[, c("name", "age", "bounty", "height")]
library(tidyr)
```

*** =sample_code
```{r}
# straw_hat_wide_df 、 tidyr已預先載入

# 轉置
straw_hat_long_df <- gather(__, key = __, value = __, __, __)

# 看看 straw_hat_long_df 前六列


```

*** =solution
```{r}
# straw_hat_wide_df 、 tidyr已預先載入

# 轉置
straw_hat_long_df <- gather(straw_hat_wide_df, key = cate, value = int, height, age)

# 看看 straw_hat_long_df 前六列
head(straw_hat_long_df)

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `gather()` &#20989;&#25976;&#23559;&#23532;&#36039;&#26009;&#26694;&#36681;&#25563;&#25104;&#38263;&#36039;&#26009;&#26694; `straw_hat_long_df`&#65311;"
test_object("straw_hat_long_df", 
            undefined_msg = msg, 
            incorrect_msg = msg) 

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `head()` &#20989;&#25976;&#30475;&#30475;&#29983;&#25104;&#30340; `straw_hat_long_df`&#65311;"
test_output_contains("head(straw_hat_long_df)",
                     incorrect_msg = msg)

success_msg("&#22826;&#26834;&#20102;&#65292;&#25105;&#20497;&#24050;&#32147;&#23416;&#26371;&#20102;&#23532;&#36039;&#26009;&#26694;&#35722;&#38263;&#36039;&#26009;&#26694;&#65292;&#25509;&#33879;&#20358;&#23416;&#24590;&#40636;&#25226;&#38263;&#36039;&#26009;&#26694;&#35722;&#25104;&#23532;&#36039;&#26009;&#26694;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4
## 資料轉置：長變寬

完成這個練習你的資料整理懸賞金額就可以提升至數千萬貝里，成為名副其實能夠跟草帽海賊團相抗衡的**超新星世代**！

進行長資料框轉置為寬資料框時我們使用同樣源於 [tidyr](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1) 套件的
[spread()](http://www.rdocumentation.org/packages/tidyr/versions/0.5.1/topics/spread) 函數。函數必須要指定幾個參數，第一個是長資料框名稱，而 `key = ` 是用來儲存**數值種類**的欄位名稱，`value = ` 是用來儲存**數值**的欄位名稱：

```{r}
spread(df_long, key = cate_col, value = num_col)
```

*** =instruction
- 使用 `head()` 函數看看 `straw_hat_long_df`
- 使用 `spread()` 函數把上一個練習生成的 `straw_hat_long_df` 轉置為 `straw_hat_wide_df`。
- 使用 `head()` 函數看看生成的資料框。

*** =hint
- `spread()` 函數的參數要指派 `straw_hat_wide_df, key = cate, value = int`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
straw_hat_wide_df <- straw_hat_df[, c("name", "age", "bounty", "height")]
straw_hat_long_df <- gather(straw_hat_wide_df, key = cate, value = int, height, age)
library(tidyr)
```

*** =sample_code
```{r}
# straw_hat_long_df 、 tidyr 已預先載入

# 看 straw_hat_long_df 前六列


# 轉置
straw_hat_wide_df <- spread(__, key = __, value = __)

# 看看 straw_hat_wide_df 前六列


```

*** =solution
```{r}
# straw_hat_long_df 、 tidyr 已預先載入

# 看 straw_hat_long_df 前六列
head(straw_hat_long_df)

# 轉置
straw_hat_wide_df <- spread(__, key = __, value = __)

# 看看 straw_hat_wide_df 前六列
head(straw_hat_wide_df)

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `head()` &#20989;&#25976;&#35264;&#23519; `straw_hat_long_df`&#65311;"
test_output_contains("head(straw_hat_long_df)",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `spread()` &#20989;&#25976;&#23559;&#23532;&#36039;&#26009;&#26694;&#36681;&#25563;&#25104;&#38263;&#36039;&#26009;&#26694; `straw_hat_wide_df`&#65311;"
test_object("straw_hat_wide_df", 
            undefined_msg = msg, 
            incorrect_msg = msg) 

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `head()` &#20989;&#25976;&#35264;&#23519; `straw_hat_wide_df`&#65311;"
test_output_contains("head(straw_hat_wide_df)",
                     incorrect_msg = msg)
success_msg("&#24685;&#21916;&#65292;&#20320;&#30340;&#25080;&#36062;&#37329;&#38989;&#24050;&#32147;&#36948;&#21040;&#25976;&#21315;&#33836;&#35997;&#37324;&#20102;&#65281;&#25509;&#19979;&#20358;&#20320;&#35201;&#33322;&#34892;&#21040;&#26368;&#24460;&#19968;&#24231;&#23798;&#23996;&#65292;&#36890;&#36942;&#35430;&#29001;&#20043;&#24460;&#20320;&#23559;&#25104;&#28858;&#25080;&#36062;&#37329;&#38989;&#25976;&#20740;&#35997;&#37324;&#65292;&#35731;&#28023;&#36557;&#38957;&#30171;&#30340;&#36229;&#32026;&#28023;&#36042;&#65281;")
```