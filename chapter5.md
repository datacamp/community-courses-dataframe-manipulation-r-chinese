---
title_meta  : 第五章
title       : 聯結資料框
description : 在一個資料分析專案中，資料可能散落在多個資料框中，因此對於資料框的聯結你必須要有清晰的認知，假如你使用過關聯式資料庫進行資料查詢，你在這章節的練習中會覺得駕輕就熟；假如你沒有使用過也不要緊，我們將在本章節學習這些技巧與概念，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:4aa0c0c890
## 惡魔果實的資料框

**惡魔果實**是海賊王世界的奇特果實，有「海上惡魔的化身」的別稱，可以讓食用者得到特殊能力，擁有惡魔果實的人普遍被叫作「惡魔果實能力者」。在草帽海賊團中有 4 個能力者，但你注意到我們並沒有一個欄位紀錄船員的惡魔果實資訊，於是你駭入海軍的機密資料庫取得了草帽海賊團的惡魔果實資料 `straw_hat_devil_fruit`。

*** =instruction
- 將草帽海賊團的惡魔果實資料框輸出在 R Console。

*** =hint
- 在編輯區輸入 `straw_hat_devil_fruit` 即可。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_devil_fruit 已預先載入

# 在 R Console 輸出 straw_hat_devil_fruit

```

*** =solution
```{r}
# straw_hat_devil_fruit 已預先載入

# 在 R Console 印出 straw_hat_devil_fruit
straw_hat_devil_fruit
```

*** =sct
```{r}
test_output_contains("straw_hat_devil_fruit",
                     times = 1,
                     incorrect_msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#25226; `straw_hat_devil_fruit` &#36664;&#20986;&#22312; R Console&#65311;")
                     
success_msg("&#23565;&#20320;&#36889;&#20301;&#34987;&#25976;&#21315;&#33836;&#35997;&#37324;&#25080;&#36062;&#30340;&#28023;&#36042;&#32780;&#35328;&#36889;&#32244;&#32722;&#23526;&#22312;&#26159;&#19968;&#29255;&#34507;&#31957;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:84d7738b12
## 內部聯結

現在你手邊已經取得了 `straw_hat_devil_fruit`，接著你想要把惡魔果實的資訊加入原本的資料框中。R 語言使用 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數來進行資料框的聯結，如果你沒有使用過關聯式資料資料庫，你可以想像一下 Excel 的 vlookup 函數功能。

```{r}
merge(df1, df2, by = col_name, ...)
```

`by = ` 參數要指定兩個資料框參照的欄位，由於我們的資料框要參照的欄位名稱是相同的： `name`，因此在使用 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數實不需要指定 `by = ` 參數。

輸出的結果會保留兩個資料框中有參照到的觀測值，這就是俗稱的**內部聯結**！

*** =instruction
- 使用 `merge()` 函數聯結 `straw_hat_df` 與 `straw_hat_devil_fruit`，將聯結後資料框宣告為 `straw_hat_df_devil_fruit`。
- 將 `straw_hat_df_devil_fruit` 輸出在 R Console。

*** =hint
- 輸入 `straw_hat_df_devil_fruit <- merge(straw_hat_df, straw_hat_devil_fruit)` 就可以完成。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 聯結資料框
straw_hat_df_devil_fruit <-

# 將結果輸出在 R Console

```

*** =solution
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 聯結資料框
straw_hat_df_devil_fruit <- merge(straw_hat_df, straw_hat_devil_fruit)

# 將結果輸出在 R Console
straw_hat_df_devil_fruit

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `merge()` &#20989;&#25976;&#29983;&#25104; `straw_hat_df_devil_fruit`&#65311;"
test_object("straw_hat_df_devil_fruit", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#22312; R Console &#36664;&#20986; `straw_hat_df_devil_fruit`&#65311;"
test_output_contains("straw_hat_df_devil_fruit",
                     incorrect_msg = msg)

success_msg("&#22826;&#26834;&#20102;&#65292;&#35264;&#23519;&#19968;&#19979;&#20320;&#30340;&#36664;&#20986;&#65292;&#20839;&#37096;&#32879;&#32080;&#21482;&#26371;&#20445;&#30041;&#20841;&#20491;&#36039;&#26009;&#26694;&#26377;&#21443;&#29031;&#21040;&#30340;&#35264;&#28204;&#20540;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:5200a77316
## 左外部聯結

回憶前一個練習最後的輸出，我們原本的資料框有 9 個船員，但是其中只有 4 個船員是惡魔果實能力者，因此當 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數沒有做其他參數設定時，預設即為**內部聯結**，輸出結果只會有兩個資料框交集的船員。

如果想要保留所有船員的資料，要在 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數中額外指定參數 `all.x = TRUE` 請 R 語言將第一個資料框的所有觀測值都保留下來：

```{r}
merge(df1, df2, all.x = TRUE)
```

輸出的結果會保留第一個資料框中的所有觀測值，而參照不到惡魔果實的船員會以遺漏值記錄，這就是俗稱的**左外部聯結**！

*** =instruction
- 使用 `merge()` 函數將 `straw_hat_df` 與 `straw_hat_devil_fruit` 進行左外部聯結，將聯結後資料框宣告為 `straw_hat_df_devil_fruit`。
- 將 `straw_hat_df_devil_fruit` 輸出在 R Console。

*** =hint
- `merge()` 函數要設定 `all.x = TRUE`。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 左外部聯結
straw_hat_df_devil_fruit <- 

# 將結果輸出在 R Console

```

*** =solution
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 左外部聯結
straw_hat_df_devil_fruit <- merge(straw_hat_df, straw_hat_devil_fruit, all.x = TRUE)

# 將結果輸出在 R Console
straw_hat_df_devil_fruit
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `merge()` &#20989;&#25976;&#29983;&#25104;&#24038;&#22806;&#37096;&#32879;&#32080;&#30340;&#32080;&#26524;&#65311;"
test_object("straw_hat_df_devil_fruit", 
            undefined_msg = msg, 
            incorrect_msg = msg) 

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559; `straw_hat_df_devil_fruit`&#36664;&#20986;&#22312; R Console&#65311;"
test_output_contains("straw_hat_df_devil_fruit",
                     incorrect_msg = msg)

success_msg("&#35264;&#23519;&#19968;&#19979;&#24038;&#22806;&#37096;&#32879;&#32080;&#29983;&#25104;&#30340;&#32080;&#26524;&#65292;&#27880;&#24847;&#27794;&#26377;&#21443;&#29031;&#21040;&#30340;&#35264;&#28204;&#20540;&#26371;&#20197;&#36986;&#28431;&#20540;&#26041;&#24335;&#35352;&#37636;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:cf1c36b9fc
## 右外部聯結

與前一個練習相呼應，既然有保留第一個資料框所有觀測值的左外部聯結，我們一定也有保留第二個資料框所有觀測值的**右外部聯結**。想要保留所有惡魔果實能力者的資料，要在 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數中額外指定參數 `all.y = TRUE` 請 R 語言將第二個資料框的所有觀測值都保留下來：

```{r}
merge(df1, df2, all.y = TRUE)
```

為了展示**右外部聯結**的效果，我們稍微修改了第一個資料框 `straw_hat_df` 留下四個船員的角色設定，兩個能力者與兩個非能力者。輸出的結果會保留第二個資料框中的所有觀測值，而參照不到主要角色設定的惡魔果實能力者欄位會以遺漏值記錄，這就是俗稱的**右外部聯結**！

*** =instruction
- 先將修改後的 `straw_hat_df` 輸出在 R Console 看看。
- 使用 `merge()` 函數將 `straw_hat_df` 與 `straw_hat_devil_fruit` 進行右外部聯結，將聯結後資料框宣告為 `straw_hat_df_devil_fruit`。
- 將 `straw_hat_df_devil_fruit` 輸出在 R Console。

*** =hint
- `merge()` 函數要設定 `all.y = TRUE`。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
straw_hat_df <- straw_hat_df[c(1:3, 6), ]
```

*** =sample_code
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 將 straw_hat_df 輸出在 R Console


# 右外部聯結
straw_hat_df_devil_fruit <- 

# 將結果輸出在 R Console

```

*** =solution
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 將 straw_hat_df 輸出在 R Console
straw_hat_df

# 右外部聯結
straw_hat_df_devil_fruit <- merge(straw_hat_df, straw_hat_devil_fruit, all.y = TRUE)

# 將結果輸出在 R Console
straw_hat_df_devil_fruit
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559; `straw_hat_df` &#36664;&#20986;&#22312; R Console&#65311;"
test_output_contains("straw_hat_df",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `merge()` &#20989;&#25976;&#36914;&#34892;&#21491;&#22806;&#37096;&#32879;&#32080;&#65311;"
test_object("straw_hat_df_devil_fruit", 
            undefined_msg = msg, 
            incorrect_msg = msg) 
                     
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559; `straw_hat_df_devil_fruit` &#36664;&#20986;&#22312; R Console&#65311;"
test_output_contains("straw_hat_df_devil_fruit",
                     incorrect_msg = msg)

success_msg("&#22826;&#26834;&#20102;&#65292;&#36996;&#24046;&#19968;&#20491;&#32244;&#32722;&#20320;&#30340;&#36039;&#26009;&#26694;&#32879;&#32080;&#25216;&#33021;&#23601;&#21487;&#20197;&#34987;&#40670;&#28415;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:69321d3583
## 全外部聯結

既然有保留第一個資料框所有觀測值的左外部聯結，亦有保留第二個資料框所有觀測值的右外部聯結，聰明如你一定想到我們必定有保留兩個資料框所有觀測值的聯結，你的推測沒有錯，那就是俗稱的**全外部聯結**，在 [merge()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/merge) 函數中額外指定參數 `all.x = TRUE` 以及 `all.y = TRUE` 請 R 語言將兩個資料框的所有觀測值都保留下來：

```{r}
merge(df1, df2, all.x = TRUE, all.y = TRUE)
```

*** =instruction
- 先將修改後的 `straw_hat_df` 輸出在 R Console 看看。
- 使用 `merge()` 函數將 `straw_hat_df` 與 `straw_hat_devil_fruit` 進行全外部聯結，將聯結後資料框宣告為 `straw_hat_df_devil_fruit`。
- 將 `straw_hat_df_devil_fruit` 輸出在 R Console。

*** =hint
- `merge()` 函數要設定 `all.x = TRUE, all.y = TRUE`。

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
straw_hat_df <- straw_hat_df[c(1:3, 6), ]
```

*** =sample_code
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 將 straw_hat_df 輸出在 R Console
straw_hat_df

# 全外部聯結
straw_hat_df_devil_fruit <- 

# 將結果輸出在 R Console
straw_hat_df_devil_fruit
```

*** =solution
```{r}
# straw_hat_df 與 straw_hat_devil_fruit 已預先載入

# 將 straw_hat_df 輸出在 R Console
straw_hat_df

# 全外部聯結
straw_hat_df_devil_fruit <- merge(straw_hat_df, straw_hat_devil_fruit, all.x = TRUE, all.y = TRUE)

# 將結果輸出在 R Console
straw_hat_df_devil_fruit
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#23559; `straw_hat_df` &#36664;&#20986;&#22312; R Console&#65311;"
test_output_contains("straw_hat_df",
                     incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `merge()` &#20989;&#25976;&#36914;&#34892;&#21491;&#22806;&#37096;&#32879;&#32080;&#65311;"
test_object("straw_hat_df_devil_fruit", 
            undefined_msg = msg, 
            incorrect_msg = msg) 

msg = "&#30906;&#35469;&#20320;&#26159;&#21542;&#26377;&#23559; `straw_hat_df_devil_fruit` &#36664;&#20986;&#22312; R Console&#65311;"
test_output_contains("straw_hat_df_devil_fruit",
                     incorrect_msg = msg)
success_msg("&#24685;&#21916;&#20320;&#65292;&#20320;&#24050;&#32147;&#25104;&#28858;&#36039;&#26009;&#32879;&#32080;&#30340;&#39640;&#25163;&#65292;&#26597;&#19968;&#19979;&#28023;&#36557;&#30340;&#36039;&#26009;&#24235;&#65292;&#20320;&#24050;&#32147;&#34987;&#21015;&#20837;&#19978;&#20740;&#36062;&#37329;&#30340;&#37325;&#40670;&#36890;&#32221;&#21517;&#21934;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:65494f3253
## 多個參照欄位的例子



*** =instruction

*** =hint

*** =pre_exercise_code

*** =sample_code

*** =solution

*** =sct