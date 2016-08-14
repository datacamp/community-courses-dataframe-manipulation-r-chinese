---
title_meta  : 第二章
title       : 欄位相關的技巧
description : 實務上我們很常會有新增變數、刪除變數或者重新命名變數...等等的需求，在資料框的結構中，其實就是針對欄位進行整理，我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:297843af96
## 新增欄位

草帽海賊團的廚師賓什莫克·香吉士要為船員們準備餐點，卻發現主要角色設定遺漏了大家最喜愛的料理，讓我們來幫助香吉士，將最喜愛的料理 `favorite_food` 加入 `straw_hat_df` 中。

*** =instructions
- 將右邊編輯區已經定義好的 `favorite_food` 向量加入 `straw_hat_df` 中。

*** =hint
- 在編輯區鍵入 `straw_hat_df$favorite_food <- favorite_food`

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 最喜愛料理的向量
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")

# 將向量加入資料框中成為新的欄位
straw_hat_df$favorite_food <- 
```

*** =solution
```{r}
# 最喜愛料理的向量
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")

# 將向量加入資料框中成為新的欄位
straw_hat_df$favorite_food <- favorite_food
```

*** =sct
```{r}
test_object(favorite_food,
            undefined_msg = "&#19981;&#38656;&#35201;&#21034;&#38500;&#21407;&#26412;&#24171;&#20320;&#23450;&#32681;&#22909;&#30340;&#21521;&#37327;&#65281;", 
            incorrect_msg = "&#19981;&#38656;&#35201;&#21034;&#38500;&#21407;&#26412;&#24171;&#20320;&#23450;&#32681;&#22909;&#30340;&#21521;&#37327;&#65281;") 

test_object(straw_hat_df$favorite_food, 
            eq_condition = "equivalent", 
            eval = TRUE, 
            undefined_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#30340;&#21521;&#37327;&#21152;&#20837;&#36039;&#26009;&#26694;&#20013;&#25104;&#28858;&#26032;&#30340;&#27396;&#20301;&#65311;", 
            incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#30340;&#21521;&#37327;&#21152;&#20837;&#36039;&#26009;&#26694;&#20013;&#25104;&#28858;&#26032;&#30340;&#27396;&#20301;&#65311;")

success_msg("&#20320;&#24171;&#20102;&#39321;&#21513;&#22763;&#19968;&#20491;&#22823;&#24537;&#65292;&#36889;&#27171;&#20182;&#25165;&#30693;&#36947;&#35442;&#28310;&#20633;&#21738;&#20123;&#26009;&#29702;&#65292;&#22826;&#26834;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4
## 刪除欄位

你在前一個練習中已經幫賓什莫克·香吉士解決了問題，你突然又覺得最喜愛的料理這個資訊無關痛癢。這樣子確實十分地善變，但是現實生活中你的主管或你的同事很可能也是如此的善變呢！讓我們將最喜愛的料理 `favorite_food` 從 `straw_hat_df` 中移除，在 R 語言中要將資料框中的欄位移除非常容易，只需要把該欄位指派為 NULL 即可：

```{r}
df$column_to_delete <- NULL
```

*** =instructions
- 將 `straw_hat_df$favorite_food` 欄位從 `straw_hat_df` 中移除。

*** =hint
- 在編輯區鍵入 `straw_hat_df$favorite_food <- NULL`

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
# 最喜愛料理的向量
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")
# 將向量加入資料框中成為新的欄位
straw_hat_df$favorite_food <- favorite_food
```

*** =sample_code
```{r}
# 刪除最喜愛料理的欄位

```

*** =solution
```{r}
# 刪除最喜愛料理的欄位
straw_hat_df$favorite_food <- NULL
```

*** =sct
```{r}
test_student_typed(c("straw_hat_df$favorite_food <- NULL", "straw_hat_df$favorite_food = NULL", 
                     "straw_hat_df$favorite_food<-NULL", "straw_hat_df$favorite_food=NULL"),
                   not_typed_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#30340;&#27396;&#20301;&#25351;&#27966;&#32102; NULL&#65311;")

success_msg("&#22826;&#22909;&#20102;&#65292;&#19981;&#31649;&#20854;&#20182;&#20154;&#22810;&#40637;&#21892;&#35722;&#65292;&#26032;&#22686;&#21034;&#38500;&#27396;&#20301;&#37117;&#38627;&#19981;&#20498;&#20320;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4
## 刪除欄位（2）

還記得我們在 [R 語言導論]()中有提到一個便利的 `subset()` 函數嗎？我們也可以利用它來刪除欄位，只要在想要刪除的欄位名稱前面加上**減號**，而且它還提供了更進階的功能，讓你可以一次刪除多個欄位！

```{r}
df <- subset(df, select = -col1)
df <- subset(df, select = c(-col1, -col2, ...))
```

*** =instructions
- 利用 `subset()` 函數寫一行程式將職業 `straw_hat_df$occupation` 與身高 `straw_hat_df$height` 從 `straw_hat_df` 中移除。

*** =hint
- 在編輯區鍵入 `straw_hat_df <- subset(straw_hat_df, select = c(-occupation, -height))`

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 用 subset 函數一次刪除職業與身高兩個欄位

```

*** =solution
```{r}
# 用 subset 函數一次刪除職業與身高兩個欄位
straw_hat_df <- subset(straw_hat_df, select = c(-occupation, -height))
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#27491;&#30906;&#22320;&#20351;&#29992; `subset()` &#20989;&#25976;&#65311;"
test_function("subset", args = c("x", "select"),
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#20351;&#29992; `subset()` &#20989;&#25976;&#21034;&#38500;&#20102;&#32887;&#26989;&#33287;&#36523;&#39640;&#20841;&#20491;&#27396;&#20301;&#65311;"
test_object(straw_hat_df,
            undefined_msg = msg, 
            incorrect_msg = msg) 

success_msg("&#22826;&#26834;&#20102;&#65292;&#38500;&#20102;&#21487;&#20197;&#30452;&#25509;&#25351;&#23450;&#27396;&#20301;&#30340;&#21517;&#31281;&#65292;&#20320;&#20063;&#21487;&#20197;&#29992;&#32034;&#24341;&#20540;&#20358;&#25351;&#23450;&#65292;&#26377;&#31354;&#21487;&#20197;&#22312; R Console &#20013;&#32244;&#32722;&#65281;")
```