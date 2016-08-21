---
title_meta  : 第一章
title       : 建立資料框
description : 在學習資料框的整理技巧之前，我們得先在 R 語言的工作環境中建立出可供我們練習的資料框才行，首先我們會複習一下在 R 語言導論中學過的內容，像是建立一個資料框，以及一些快速探索資料框的好用函數，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:9a073c3931
## 建立資料框

我們會用到很多 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.xZfVkjM)中的觀念與語法，非常建議你在開始本課程之前先去玩玩看 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.xZfVkjM)唷！

草帽海賊團主要角色設定有：

- 姓名
- 性別
- 職業
- 賞金
- 年齡
- 生日
- 身高

建立資料框之前，通常我們習慣先將各個欄位生成為向量，我們大概猜想得到姓名應該是字串型的向量，而年齡會是數值型的向量。資料框特性是可以容納不同的資料格式，這代表著我們可以生成一個資料框將所有的角色設定都記錄在其中。

*** =instructions
- 使用 `data.frame()` 將右邊編輯區已經定義好的角色設定向量結合為一個資料框，並命名為 `straw_hat_df`。

*** =hint
- 在編輯區鍵入 `straw_hat_df <- data.frame(name, gender, occupation, bounty, age, birthday, height)`

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

success_msg("&#20320;&#20570;&#24471;&#22826;&#26834;&#20102;&#65292;&#35731;&#25105;&#20497;&#32380;&#32396;&#33322;&#21521;&#19979;&#19968;&#20491;&#23798;&#23996;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:cb3400c7e4
## 探索資料框

我們可以使用幾個好用的函數來快速探索一個資料框：

- `dim()`
- `head()`
- `tail()`
- `str()`
- `summary()`

`dim()` 函數會回傳資料框的列數與欄數；`head()` 函數會回傳資料框的前六列；`tail()` 函數會回傳資料框的後六列；`str()` 函數不僅會回傳資料框的列數與欄數，還會列出每個欄位的資料類型以及前幾個觀測值；`summary()` 函數會回傳每個欄位的敘述性統計資料。

*** =instructions
- 使用這 5 個好用的函數探索已經載入工作環境的 `straw_hat_df`。

*** =hint
- 使用 `dim(straw_hat_df)` 、 `head(straw_hat_df)` 、 `tail(straw_hat_df)` 、 `str(straw_hat_df)` 與 `summary(straw_hat_df)` 探索資料框。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 資料框已經預先載入

# 對 straw_hat_df 使用 `dim()` 、 `head()` 、 `tail()` 、 `str()` 與 `summary()`

```

*** =solution
```{r}
# straw_hat_df 資料框已經預先載入

# 對 straw_hat_df 使用 `dim()` 、 `head()` 、 `tail()` 、 `str()` 與 `summary()`
dim(straw_hat_df)
head(straw_hat_df)
tail(straw_hat_df)
str(straw_hat_df)
summary(straw_hat_df)
```

*** =sct
```{r}
test_function("dim", "x", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `dim()` &#20989;&#25976;&#65311;")
test_output_contains("dim(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `dim()` &#20989;&#25976;&#65311;")

test_function("head", "x", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `head()` &#20989;&#25976;&#65311;")
test_output_contains("head(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `head()` &#20989;&#25976;&#65311;")

test_function("tail", "x", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `tail()` &#20989;&#25976;&#65311;")
test_output_contains("tail(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `tail()` &#20989;&#25976;&#65311;")

test_function("str", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `str()` &#20989;&#25976;&#65311;")
test_output_contains("str(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `str()` &#20989;&#25976;&#65311;")

test_function("summary", "x", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `summary()` &#20989;&#25976;&#65311;")
test_output_contains("summary(straw_hat_df)", incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#23565; `straw_hat_df` &#20351;&#29992; `summary()` &#20989;&#25976;&#65311;")

success_msg("&#22826;&#26834;&#20102;&#65292;&#24819;&#24517;&#20320;&#24050;&#32147;&#36843;&#19981;&#21450;&#24453;&#35201;&#33322;&#21521;&#19979;&#19968;&#20491;&#23798;&#23996;&#65292;&#25509;&#19979;&#20358;&#25105;&#20497;&#35201;&#25361;&#25136;&#36319;&#27396;&#20301;&#30456;&#38364;&#30340;&#25216;&#24039;&#65281;");
```