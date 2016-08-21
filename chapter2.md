---
title_meta  : 第二章
title       : 欄與列的相關技巧
description : 實務上我們很常會有新增變數、刪除變數或者篩選觀測值...等等的需求，在資料框的結構中，其實就是針對欄或者列進行整理，我們將在本章節學習這些技巧，一場爭奪 One Piece 的海上冒險故事！

--- type:NormalExercise lang:r xp:100 skills:4 key:297843af96
## 新增欄位

草帽海賊團的廚師賓什莫克·香吉士要為船員們準備餐點，卻發現主要角色設定遺漏了大家最喜愛的料理，於是他向可愛的讀者求助，就讓我們來幫助他將最喜愛的料理 `favorite_food` 加入 `straw_hat_df` 中。

*** =instructions
- 將右邊編輯區已經定義好的 `favorite_food` 向量加入 `straw_hat_df` 中。

*** =hint
- 在編輯區鍵入 `straw_hat_df$favorite_food <- favorite_food`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
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
            undefined_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#30340;&#21521;&#37327;&#21152;&#20837;&#36039;&#26009;&#26694;&#20013;&#25104;&#28858;&#26032;&#30340;&#27396;&#20301;&#65311;", 
            incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#30340;&#21521;&#37327;&#21152;&#20837;&#36039;&#26009;&#26694;&#20013;&#25104;&#28858;&#26032;&#30340;&#27396;&#20301;&#65311;")

success_msg("&#20320;&#24171;&#20102;&#39321;&#21513;&#22763;&#19968;&#20491;&#22823;&#24537;&#65292;&#36889;&#27171;&#20182;&#25165;&#30693;&#36947;&#35442;&#28310;&#20633;&#21738;&#20123;&#26009;&#29702;&#65292;&#22826;&#26834;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:142b366f49
## 新增欄位（2）

R 語言有一個很可愛的特性是**殊途同歸**，做同樣一件事情，可能有多種方式可以達成。在這個練習中我們要介紹如何使用 [cbind()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/cbind) 這個函數來將最喜愛的料理 `favorite_food` 加入 `straw_hat_df` 中。

```{r}
df <- cbind(df, column_to_add)
```

*** =instructions
- 將右邊編輯區已經定義好的 `favorite_food` 向量利用 `cbind()` 函數加入 `straw_hat_df` 中。

*** =hint
- 在編輯區鍵入 `straw_hat_df <- cbind(straw_hat_df, favorite_food)`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# 最喜愛料理的向量
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")

# 利用 cbind() 函數將向量加入資料框中成為新的欄位
straw_hat_df <- 
```

*** =solution
```{r}
# 最喜愛料理的向量
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")

# 利用 cbind() 函數將向量加入資料框中成為新的欄位
straw_hat_df <- cbind(straw_hat_df, favorite_food)
```

*** =sct
```{r}
test_object(favorite_food,
            undefined_msg = "&#19981;&#38656;&#35201;&#21034;&#38500;&#21407;&#26412;&#24171;&#20320;&#23450;&#32681;&#22909;&#30340;&#21521;&#37327;&#65281;", 
            incorrect_msg = "&#19981;&#38656;&#35201;&#21034;&#38500;&#21407;&#26412;&#24171;&#20320;&#23450;&#32681;&#22909;&#30340;&#21521;&#37327;&#65281;") 

test_function("cbind", 
               incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `cbind()` &#20989;&#25976;&#65311;")

test_object(straw_hat_df$favorite_food, 
            undefined_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `cbind()` &#20989;&#25976;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#26032;&#22686;&#33267;&#36039;&#26009;&#26694;&#65311;", 
            incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `cbind()` &#20989;&#25976;&#23559;&#26368;&#21916;&#24859;&#26009;&#29702;&#26032;&#22686;&#33267;&#36039;&#26009;&#26694;&#65311;")

success_msg("&#22826;&#26834;&#20102;&#65292;&#23416;&#26371;&#26032;&#22686;&#20043;&#24460;&#25105;&#20497;&#20358;&#23416;&#32722;&#22914;&#20309;&#21034;&#38500;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:c8c237a023
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
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
favorite_food <- c("肉", "搭配酒的食物", "橘子", "魚", "搭配紅茶的食物", "甜食", "搭配咖啡的食物", "搭配可樂的食物", "牛奶")
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

--- type:NormalExercise lang:r xp:100 skills:4 key:c78ba59b50
## 刪除欄位（2）

還記得我們在 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.FaeP7Yg)中有提到一個便利的 [subset()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/subset) 函數嗎？我們也可以利用它來刪除欄位，只需在想要刪除的欄位名稱前面加上**減號**，而且它還提供了更進階的功能，讓你可以一次刪除多個欄位！

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
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
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

--- type:NormalExercise lang:r xp:100 skills:4 key:ccfe68db30
## 為欄位重新命名

R 語言可以使用 [names()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/names) 函數將資料框的欄位名稱用向量的格式輸出：

```{r}
names(df)
```

透過指定索引值就可以對欄位重新命名：

```{r}
names(df)[1] <- "new_name_column1"
```

注意 R 語言的索引值是由 **1** 起算，這一點跟其他程式語言從 0 起算是不一樣的！

*** =instructions
- 將 `straw_hat_df` 的賞金欄位 `bounty` 改命名為 `reward`。

*** =hint
- 在編輯區鍵入 `names(straw_hat_df)[4] <- "reward"`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 資料框已預先載入

# 將賞金欄位 straw_hat_df$bounty 改命名為 straw_hat_df$reward

```

*** =solution
```{r}
# straw_hat_df 資料框已預先載入

# 將賞金欄位 straw_hat_df$bounty 改命名為 straw_hat_df$reward
names(straw_hat_df)[4] <- "reward"
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `names()` &#20989;&#25976;&#65311;"
test_function("names",
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `names()` &#20989;&#25976;&#23559; bounty &#27396;&#20301;&#25913;&#21629;&#21517;&#28858; reward&#65311;"
test_object(straw_hat_df$reward,
            undefined_msg = msg, 
            incorrect_msg = msg) 

success_msg("&#36899;&#40860;&#27611;&#30340;&#37325;&#26032;&#21629;&#21517;&#27396;&#20301;&#37117;&#38627;&#19981;&#20498;&#20320;&#65292;&#22826;&#26834;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:d3c614f19b
## 鑽研 subset() 函數

前面練習示範的刪除欄位只是 [subset()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/subset) 函數的其中一個功能。`subset()` 函數在篩選觀測值與變數非常實用，假如你想快速看到草帽魯夫的懸賞金額，可以練習在 R Console 輸入：

```{r}
subset(straw_hat_df, name == "蒙其·D·魯夫", select = c(name, bounty))
```

*** =instructions
- 將草帽海賊團賞金大於 1000 萬貝里並且年齡小於 30 歲的成員篩選出來，欄位只需要包含姓名、賞金與年齡。

*** =hint
- 在編輯區鍵入 `subset(straw_hat_df, bounty > 10000000 & age < 30, select = c(name, bounty, age))`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 資料框已預先載入

# 篩選賞金大於 1000 萬貝里並且年齡小於 30 歲，欄位只需要包含姓名、賞金與年齡

```

*** =solution
```{r}
# straw_hat_df 資料框已預先載入

# 篩選賞金大於 1000 萬貝里並且年齡小於 30 歲，欄位只需要包含姓名、賞金與年齡
subset(straw_hat_df, bounty > 10000000 & age < 30, select = c(name, bounty, age))
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `subset()` &#20989;&#25976;&#65311;"
        
test_function("subset",
               not_called_msg = msg,
               args_not_specified_msg = msg,
               incorrect_msg = msg)
               
test_output_contains("subset(straw_hat_df, bounty > 10000000 & age < 30, select = c(name, bounty, age))",
                      incorrect_msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#31721;&#36984;&#20986;&#38988;&#30446;&#25152;&#35201;&#27714;&#30340;&#35264;&#28204;&#20540;&#33287;&#27396;&#20301;&#65311;")

success_msg("&#22826;&#26834;&#20102;&#65292;`subset()` &#20989;&#25976;&#26159;&#24375;&#32780;&#26377;&#21147;&#30340;&#24037;&#20855;&#65292;&#23427;&#33021;&#22816;&#35731;&#20320;&#26356;&#26377;&#25928;&#29575;&#22320;&#34389;&#29702;&#36039;&#26009;&#26694;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:2de6bd4bcf
## 新增列數

前面練習我們介紹了 [cbind()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/subset) 函數能夠協助新增欄位，聰明的你一定能夠舉一反三想到那是不是也有相對應的函數可以協助新增列數呢？沒有錯，R 語言的確有相對應的 [rbind()](http://www.rdocumentation.org/packages/R6Frame/versions/0.1.0/topics/rbind) 函數：

```{r}
df <- rbind(df, row_to_add)
```

鄉民們對於第十位船員的猜測議論紛紛，各種神預測，在這裡我們稍微懷舊一下，草帽海賊團永遠的夥伴：阿拉巴斯坦王國的薇薇公主。

*** =instructions
- 利用 `rbind()` 將薇薇公主加入草帽海賊團資料框。

*** =hint
- 在編輯區鍵入 `straw_hat_df <- rbind(straw_hat_df, princess_vivi)`

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_devil_fruit.RData"))
```

*** =sample_code
```{r}
# straw_hat_df 資料框已預先載入

# 薇薇公主
princess_vivi <- c("奈菲魯塔莉·薇薇", "女", "公主", NA, 18, "02-02", NA)

# 將薇薇公主加入草帽海賊團資料框
straw_hat_df <- 
```

*** =solution
```{r}
# straw_hat_df 資料框已預先載入

# 薇薇公主
princess_vivi <- c("奈菲魯塔莉·薇薇", "女", "公主", NA, 18, "02-02", NA)

# 將薇薇公主加入草帽海賊團資料框
straw_hat_df <- rbind(straw_hat_df, princess_vivi)
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `rbind()` &#20989;&#25976;&#65311;"
        
test_function("rbind",
               not_called_msg = msg,
               args_not_specified_msg = msg,
               incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#23559;&#34183;&#34183;&#20844;&#20027;&#21152;&#20837;&#33609;&#24125;&#28023;&#36042;&#22296;&#36039;&#26009;&#26694;&#65311;"
               
test_object("straw_hat_df", 
             undefined_msg = NULL, 
             incorrect_msg = NULL) 

success_msg("&#33609;&#24125;&#28023;&#36042;&#22296;&#38626;&#38283;&#38463;&#25289;&#24052;&#26031;&#22374;&#29579;&#22283;&#26178;&#65292;&#32972;&#23565;&#33879;&#34183;&#34183;&#21644;&#36305;&#24471;&#24555;&#33289;&#36215;&#20102;&#30059;&#22312;&#24038;&#25163;&#33218;&#19978;&#30340; X &#35352;&#34399;&#12290;&#19981;&#31649;&#31532;&#21313;&#20491;&#22821;&#20276;&#26159;&#35504;&#65292;&#34183;&#34183;&#21644;&#36305;&#24471;&#24555;&#20173;&#34987;&#35469;&#23450;&#26159;&#33609;&#24125;&#28023;&#36042;&#22296;&#30340;&#33337;&#21729;&#65281;")
```