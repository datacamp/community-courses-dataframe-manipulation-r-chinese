---
title_meta  : 第一章
title       : 建立與探索資料框
description : 在學習資料框的整理技巧之前，我們得先在 R 語言的工作環境中建立出可供我們練習的資料框才行，在本章我們首先會複習在 R 語言導論中學過的內容，像是建立一個資料框以及一些快速探索資料框的好用函數，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:9a073c3931
## 建立資料框

本課程會用到很多 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.xZfVkjM)中的觀念與語法，非常建議你先去玩玩看 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.xZfVkjM)再開始本課程！

草帽海賊團主要角色設定有：

- 姓名
- 性別
- 職業
- 賞金
- 年齡
- 生日
- 身高

建立資料框之前通常習慣先將各個欄位生成為向量，我們大概猜想得到姓名應該是字串型的向量，而年齡會是數值型的向量。資料框特性是可以容納不同的資料格式，這代表著我們可以生成一個資料框將草帽海賊團的角色設定記錄在其中。

*** =instructions
- 使用 `data.frame()` 將右邊編輯區已經定義好的角色設定向量結合為一個資料框，並命名為 `straw_hat_df`。

*** =hint
- 在編輯區輸入 `straw_hat_df <- data.frame(name, gender, occupation, bounty, age, birthday, height)`

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# 角色設定的向量
name <- c("蒙其·D·魯夫", "羅羅亞·索隆", "娜美", "騙人布", "賓什莫克·香吉士", "多尼多尼·喬巴", "妮可·羅賓", "佛朗基", "布魯克")
gender <- c("男", "男", "女", "男", "男", "雄", "女", "男", "男")
occupation <- c("船長", "劍士", "航海士", "狙擊手", "廚師", "船醫", "考古學家", "船匠", "音樂家")
bounty <- c(500000000, 320000000, 66000000, 200000000, 177000000, 100, 130000000, 94000000, 83000000)
age <- c(19, 21, 20, 19, 21, 17, 30, 36, 90)
birthday <- c("05-05", "11-11", "07-03", "04-01", "03-02", "12-24", "02-06", "03-09", "04-03")
height <- c(174, 181, 170, 176, 180, 90, 188, 240, 277)

# 建立草帽海賊團角色設定的資料框
straw_hat_df <- 
```

*** =solution
```{r}
# 角色設定的向量
name <- c("蒙其·D·魯夫", "羅羅亞·索隆", "娜美", "騙人布", "賓什莫克·香吉士", "多尼多尼·喬巴", "妮可·羅賓", "佛朗基", "布魯克")
gender <- c("男", "男", "女", "男", "男", "雄", "女", "男", "男")
occupation <- c("船長", "劍士", "航海士", "狙擊手", "廚師", "船醫", "考古學家", "船匠", "音樂家")
bounty <- c(500000000, 320000000, 66000000, 200000000, 177000000, 100, 130000000, 94000000, 83000000)
age <- c(19, 21, 20, 19, 21, 17, 30, 36, 90)
birthday <- c("05-05", "11-11", "07-03", "04-01", "03-02", "12-24", "02-06", "03-09", "04-03")
height <- c(174, 181, 170, 176, 180, 90, 188, 240, 277)

# 建立草帽海賊團角色設定的資料框
straw_hat_df <- data.frame(name, gender, occupation, bounty, age, birthday, height)
```

*** =sct
```{r}
msg <- "&#19981;&#38656;&#35201;&#31227;&#38500;&#21407;&#26412;&#24171;&#20320;&#23450;&#32681;&#22909;&#30340;&#21521;&#37327;&#21908;&#65281;"

test_object("name", undefined_msg = msg, incorrect_msg = msg)
test_object("gender", undefined_msg = msg, incorrect_msg = msg)
test_object("occupation", undefined_msg = msg, incorrect_msg = msg)
test_object("bounty", undefined_msg = msg, incorrect_msg = msg)
test_object("age", undefined_msg = msg, incorrect_msg = msg)
test_object("birthday", undefined_msg = msg, incorrect_msg = msg)
test_object("height", undefined_msg = msg, incorrect_msg = msg)

test_object("straw_hat_df", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#20351;&#29992; `data.frame()` &#20989;&#25976;&#20006;&#19988;&#23559;&#32080;&#26524;&#25351;&#27966;&#32102; straw_hat_df&#65311;")

success_msg("&#20320;&#20570;&#24471;&#22826;&#26834;&#20102;&#65292;&#35731;&#25105;&#20497;&#32380;&#32396;&#19979;&#19968;&#20491;&#32244;&#32722;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:cb3400c7e4
## 探索資料框

我們可以使用幾個好用的函數來快速探索一個資料框：

- [`dim()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/dim) 函數
- [`head()`](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/head) 函數
- [`tail()`](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/head) 函數
- [`str()`](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/str) 函數
- [`summary()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/summary) 函數

[`dim()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/dim) 函數會回傳資料框的列數與欄數；[head()](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/head) 函數會回傳資料框的前六列；[`tail()`](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/head) 函數會回傳資料框的後六列；[`str( )`](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/str) 函數不僅會回傳資料框的列數與欄數，還會列出每個欄位的資料類型以及前幾個觀測值；[`summary()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/summary) 函數會回傳每個欄位的敘述性統計資料。

*** =instructions
- 使用這 5 個好用的函數探索已經載入工作環境的 `straw_hat_df`。

*** =hint
- 使用 `dim(straw_hat_df)` 、 `head(straw_hat_df)` 、 `tail(straw_hat_df)` 、 `str(straw_hat_df)` 與 `summary(straw_hat_df)` 探索資料框。

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv", stringsAsFactors = FALSE)
straw_hat_df$gender <- factor(straw_hat_df$gender)
```

*** =sample_code
```{r}
# straw_hat_df 已經預先載入

# 對 straw_hat_df 使用 dim() 、 head() 、 tail() 、 str() 與 summary()

```

*** =solution
```{r}
# straw_hat_df 已經預先載入

# 對 straw_hat_df 使用 dim() 、 head() 、 tail() 、 str() 與 summary()
dim(straw_hat_df)
head(straw_hat_df)
tail(straw_hat_df)
str(straw_hat_df)
summary(straw_hat_df)
```

*** =sct
```{r}
test_output_contains("dim(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `dim()` &#20989;&#25976;&#65311;")

test_output_contains("head(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `head()` &#20989;&#25976;&#65311;")

test_output_contains("tail(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `tail()` &#20989;&#25976;&#65311;")

test_output_contains("str(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `str()` &#20989;&#25976;&#65311;")

test_output_contains("summary(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `summary()` &#20989;&#25976;&#65311;")

success_msg("&#22826;&#26834;&#20102;&#65292;&#36889;&#20123;&#20989;&#25976;&#37117;&#38750;&#24120;&#23526;&#29992;&#65292;&#19968;&#23450;&#35201;&#25226;&#23427;&#20497;&#35352;&#36215;&#20358;&#65281;");
```

--- type:NormalExercise lang:r xp:100 skills:4 key:92e28431f1
## 依據欄位排序資料框

有時候我們對於資料框的外觀與排列會有自己的意見，例如會希望依照字母順序或者年齡大小的方式排序，在 R 語言可以使用 [`order()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/order) 函數來實現：

```{r}
df[order(df$col, decreasing = FALSE)]
```

[`order()`](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/order) 函數預設都是**遞增排序**，所以 `decreasing = ` 的參數預設為 `FALSE`，如果我們希望是**遞減排序**就必須將參數設為 `decreasing = TRUE`。

*** =instructions
- 用 `height` 遞增排序草帽海賊團資料框。
- 用 `bounty` 遞減排序草帽海賊團資料框。

*** =hint
- `decreasing = ` 設為 `FALSE` 或者不指定參數沿用預設。
- `decreasing = ` 設為 `TRUE`。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))

```

*** =sample_code
```{r}
# straw_hat_df 已經預先載入

# 用 height 遞增排序
straw_hat_df[order(straw_hat_df$__, decreasing = __), ]

# 用 bounty 遞減排序
straw_hat_df[order(straw_hat_df$__, decreasing = __), ]

```

*** =solution
```{r}
# straw_hat_df 已經預先載入

# 用 height 遞增排序
straw_hat_df[order(straw_hat_df$height, decreasing = FALSE), ]

# 用 bounty 遞減排序
straw_hat_df[order(straw_hat_df$bounty, decreasing = TRUE), ]

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `order()` &#20989;&#25976;&#23565;&#36523;&#39640;&#20570;&#36958;&#22686;&#25490;&#24207;&#65311;"
test_output_contains("straw_hat_df[order(straw_hat_df$height, decreasing = FALSE), ]",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `order()` &#20989;&#25976;&#23565;&#36062;&#37329;&#20570;&#36958;&#28187;&#25490;&#24207;&#65311;"
test_output_contains("straw_hat_df[order(straw_hat_df$bounty, decreasing = TRUE), ]",
                     incorrect_msg = msg)

success_msg("&#22826;&#22909;&#20102;&#65292;&#36889;&#20123;&#29105;&#36523;&#32244;&#32722;&#23565;&#20320;&#32780;&#35328;&#19968;&#23450;&#37117;&#30456;&#30070;&#23481;&#26131;&#21543;&#65311;&#28310;&#20633;&#22909;&#25105;&#20497;&#23601;&#35201;&#33322;&#21521;&#19979;&#19968;&#20491;&#23798;&#23996;&#22217;&#65281;")
```