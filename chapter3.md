---
title_meta  : 第三章
title       : 衍生欄位的相關技巧
description : 從資料庫或者既有資料的變數有時候並不能滿足我們的分析需求，於是我們常需要生成衍生變數，可能是將類別型變數重新歸類、將數值型變數歸類為類別型變數或者針對數值型變數作計算，我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:db8d80a572
## 類別型變數的重新分類

草帽海賊團的船醫多尼多尼·喬巴是吃了**人人果實**的可愛馴鹿，他對於自己的性別設定跟其他男性船員不同感到不太開心，有超高人氣的他還沒有向粉絲開口，我們就已經知道他在想什麼了，讓我們新增一個性別欄位，這個欄位只會有兩種分類：男生或者女生。

*** =instructions
- 將右邊編輯區畫底線的空位填入適當值。

*** =hint
- 我們要把原始是「男」與「雄」的值轉換為「男生」，把原始是「女」的值轉換為「女生」！

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 填入適當的值
straw_hat_df$gender_binary[straw_hat_df$gender == "__"] <- "男生"
straw_hat_df$gender_binary[straw_hat_df$gender == "__"] <- "男生"
straw_hat_df$gender_binary[straw_hat_df$gender == "__"] <- "女生"
```

*** =solution
```{r}
# 填入適當的值
straw_hat_df$gender_binary[straw_hat_df$gender == "男"] <- "男生"
straw_hat_df$gender_binary[straw_hat_df$gender == "雄"] <- "男生"
straw_hat_df$gender_binary[straw_hat_df$gender == "女"] <- "女生"
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#22312;&#30059;&#24213;&#32218;&#30340;&#22320;&#26041;&#22635;&#20837;&#27491;&#30906;&#30340;&#20540;&#65311;"

test_object("straw_hat_df$gender_binary", 
            undefined_msg = NULL, 
            incorrect_msg = NULL) 

success_msg("&#22826;&#26834;&#20102;&#65292;&#21932;&#24052;&#24456;&#38283;&#24515;&#33258;&#24049;&#30340;&#35282;&#33394;&#35373;&#23450;&#36319;&#20854;&#20182;&#20154;&#19968;&#27171;&#65292;&#20294;&#26159;&#20182;&#19981;&#22909;&#24847;&#24605;&#36319;&#25105;&#20497;&#35498;&#35613;&#35613;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:70f2080cea
## 數值型變數的分類

草帽海賊團的船員經過多雷斯羅薩決戰之後賞金大幅上升，新世界其他的海賊團無不虎視眈眈，對草帽海賊團進行戰力評估，他們想要將船員依照賞金級距切分為低、中與高三個等級，這個作法如同新增加了一個類別型變數，但卻是由既有的數值型變數所衍生得到。在 R 語言中，我們可以善用 [cut()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/cut) 函數來做這件事情。

```{r}
df$new_column <- cut(df$column, breaks = c(0, break1, break2, Inf), labels = c("label1", "label2", "label3"))
```

*** =instructions
- 新增一個變數 `bounty_level` 將賞金小於 8 千 3 百萬貝里的船員歸類為低，賞金介於 8 千 3 百萬貝里與 1 億 8 千萬貝里之間的船員歸類為中，將賞金高於 1 億 8 千萬貝里的船員歸類為高。

*** =hint
- `cut()` 函數的第一個參數要設為 `straw_hat_df$bounty`，`breaks` 的級距要加入 8 千 3 百萬貝里與 1 億 8 千萬貝里，`labels` 則是要將低、中與高依序放入！

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 填入適當的值
straw_hat_df$bounty_level <- cut(straw_hat_df$bounty, breaks = c(0, __, __, Inf), labels = c("__", "__", "__"))
```

*** =solution
```{r}
# 填入適當的值
straw_hat_df$bounty_level <- cut(straw_hat_df$bounty, breaks = c(0, 83000000, 180000000, Inf), labels = c("低", "中", "高"))
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `cut()` &#20989;&#25976;&#65311;"

test_function("cut",
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#33337;&#21729;&#20381;&#29031;&#36062;&#37329;&#20998;&#39006;&#28858;&#20302;&#20013;&#39640;&#19977;&#20491;&#32026;&#36317;&#65311;"

test_object("straw_hat_df$gender_binary", 
            undefined_msg = msg, 
            incorrect_msg = msg) 

success_msg("&#21703;&#65292;&#20320;&#24050;&#32147;&#23565;&#33609;&#24125;&#28023;&#36042;&#22296;&#30340;&#25136;&#21147;&#30637;&#33509;&#25351;&#25484;&#65292;&#20294;&#20809;&#26159;&#36889;&#27171;&#36996;&#19981;&#36275;&#20197;&#35731;&#20320;&#36319;&#20182;&#20497;&#30456;&#25239;&#34913;&#65292;&#20320;&#36996;&#38656;&#35201;&#32380;&#32396;&#24375;&#21270;&#25136;&#21147;&#65281;")
```