---
title_meta  : 第三章
title       : 衍生欄位的相關技巧
description : 從資料庫或者既有資料的變數有時候並不能滿足我們的分析需求，於是我們常需要生成衍生變數，可能是將類別型變數重新歸類、將數值型變數歸類為類別型變數或者針對數值型變數作計算，我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4
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

--- type:NormalExercise lang:r xp:100 skills:4
## 數值型變數的分類

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