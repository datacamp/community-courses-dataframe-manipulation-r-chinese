---
title_meta  : 第三章
title       : 生成衍生變數
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

--- type:NormalExercise lang:r xp:100 skills:4 key:3d3db367ea
## 衍生計算數值型變數

在前一個練習中我們對賞金進行級距的切分時你是否有感覺到單位的不便？沒錯，通常在處理較大數量級的變數時我們會轉換單位便於使用，像是千、百萬或者十億。現在就讓我們來新增一個以百萬元貝里作為單位的變數 `bounty_million`。

*** =instructions
- 將原本的 `straw_hat_df$bounty` 除以 1,000,000 並指派給一個新資料框變數 `straw_hat_df$bounty_million`。

*** =hint
- 在編輯區鍵入 `straw_hat_df$bounty_million <- straw_hat_df$bounty / 1000000`。

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 新增一個以百萬元貝里作為單位的 straw_hat_df$bounty_million
straw_hat_df$bounty_million <- 
```

*** =solution
```{r}
# 新增一個以百萬元貝里作為單位的 straw_hat_df$bounty_million
straw_hat_df$bounty_million <- straw_hat_df$bounty / 1000000
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#23559;&#36062;&#37329;&#38500;&#20197; 1 &#30334;&#33836;&#20006;&#29986;&#29983;&#19968;&#20491;&#26032;&#35722;&#25976; `bounty_million`&#65311;"
test_object("straw_hat_df$bounty_million",
            undefined_msg = msg, 
            incorrect_msg = msg) 

success_msg("&#30495;&#26159;&#22826;&#21426;&#23475;&#20102;&#65292;&#36889;&#19979;&#34893;&#29983;&#35336;&#31639;&#25976;&#20540;&#22411;&#35722;&#25976;&#20063;&#38627;&#19981;&#20498;&#20320;&#20102;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:324a377059
## 較難的衍生變數

前進新世界，邁向成為海賊王道路上的挑戰是愈來愈艱辛，在接下來的練習我們要處理有一點棘手的問題。在原始的角色設定中，我們只有船員們的年齡與生日的月份和日期，即便海賊王世界所使用的紀年與我們所熟稔的西元紀年迥異，身為超級粉絲與資料狂熱份子，你依然想要新增一個變數欄位來紀錄包含西元年份的草帽海賊團船員生日。

我們要先介紹 `Sys.Date()` 這個函數，它會回傳現在的系統日期，你可以在 R Console 輸入：

```{r}
Sys.Date()
```

R Console 會將現在的系統日期以 "%Y-%m-%d" 的格式回傳。`%Y` 代表四位數字的西元紀年，`%m` 代表兩位數字的月份，`%d` 代表兩位數字的日期。而運用 [format()](http://www.rdocumentation.org/packages/utils/versions/3.3.1/topics/format) 函數可以得到我們需要的西元年。

```{r}
format(Sys.Date(), '%Y')
```

產生出來的西元年格式是字元，如果想要做運算還需要利用 [as.numeric()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/numeric) 轉為數值。

```{r}
as.numeric(format(Sys.Date(), '%Y'))
```

*** =instructions
- 將 `Sys.Date()` 的產出指派給一個變數 `sys_date`。
- 利用 `format()` 函數將 `sys_date` 的西元年指派給 `sys_date_year`。
- 利用 `as.numeric()` 函數將 `sys_date_year` 轉換為數值並指派給 `sys_date_year_num`。

*** =hint
- `Sys.Date()` 不需要輸入參數
- `format()` 函數第二個參數必須指定為 `'%Y'`

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
```

*** =sample_code
```{r}
# 產生 sys_date
sys_date <- 

# 產生 sys_date_year
sys_date_year <- 

# 產生 sys_date_year_num
sys_date_year_num <- 

```

*** =solution
```{r}
# 產生 sys_date
sys_date <- Sys.Date()

# 產生 sys_date_year
sys_date_year <- format(sys_date, '%Y')

# 產生 sys_date_year_num
sys_date_year_num <- as.numeric(sys_date_year)

```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `Sys.Date()` &#20989;&#25976;&#29986;&#20986; `sys_date`&#65311;"
test_object("sys_date", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `format()` &#20989;&#25976;&#29986;&#20986; `sys_date_year`&#65311;"            
test_object("sys_date_year", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `as.numeric()` &#20989;&#25976;&#29986;&#20986; `sys_date_year_num`&#65311;"            
test_object("sys_date_year_num", 
            undefined_msg = msg, 
            incorrect_msg = msg)
            
success_msg("&#22826;&#22909;&#20102;&#65292;&#25509;&#19979;&#20358;&#25105;&#20497;&#35201;&#25226;&#29986;&#20986;&#30340;&#35199;&#20803;&#24180;&#20221;&#28187;&#21435;&#33337;&#21729;&#20497;&#30340;&#24180;&#40801;&#65292;&#20358;&#24471;&#21040;&#27599;&#20491;&#20154;&#30340;&#35199;&#20803;&#20986;&#29983;&#24180;&#20221;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:b1faadbe0c
## 較難的衍生變數（2）

在前一個練習我們已經生成被儲存為數值類型的系統日期西元年份，接下來我們要用每個船員各自的年齡來計算生日的西元年份，R 語言的使用者在產生衍生變數的過程不喜歡扛著整個資料框，於是我們會先將要使用於計算的變數獨立出來：

```{r}
vector1 <- df$col1
```

計算後我們會得到船員的生日西元年份，但是你忽然想起來 `birthday` 是儲存成字元的資料格式，於是在結合之前可別忘了使用 [as.character()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/character) 函數轉換為字元！

*** =instructions
```{r}
- 將年齡從資料框中選出，另外指派為一個向量 `age`。
- 將生日從資料框中選出，另外指派為一個向量 `birthday`。
- 將系統日期西元年份 `sys_date_year_num` 減去 `age` 得到各個船員的生日西元年份 `birth_year`。
- 使用 `as.character()` 將 `birth_year` 轉成字元 `birth_year_char`。
```

*** =hint
```{r}
- 輸入 `age <- straw_hat_df$age` 與 `birthday <- straw_hat_df$birthday` 將需要計算的欄位獨立出來。
- 記得使用 `as.character()` 函數。
```

*** =pre_exerise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
sys_date <- Sys.Date()
sys_date_year <- format(sys_date, '%Y')
sys_date_year_num <- as.numeric(sys_date_year)
rm(sys_date)
rm(sys_date_year)
```

*** =sample_code
```{r}
# straw_hat_df 與 sys_date_year_num 已預先載入

# 宣告 age 向量
age <- 

# 宣告 birthday 向量
birthday <- 

# 用 sys_date_year_num 減去 age 並指派給 birth_year
birth_year <- 

# 利用 as.character 將 birth_year 轉換成字元
birth_year_char <- 
```

*** =solution
```{r}
# straw_hat_df 與 sys_date_year_num 已預先載入

# 宣告 age 向量
age <- straw_hat_df$age

# 宣告 birthday 向量
birthday <- straw_hat_df$birthday

# 用 sys_date_year_num 減去 age 並指派給 birth_year
birth_year <- sys_date_year_num - age

# 利用 as.character 將 birth_year 轉換成字元
birth_year_char <- as.character(birth_year)
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#23459;&#21578; `age` &#35722;&#25976;&#65311;"
test_object("age", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#23459;&#21578; `birthday` &#35722;&#25976;&#65311;"
test_object("birthday", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#29992; `sys_date_year_num` &#28187;&#21435; `age` &#20006;&#25351;&#27966;&#32102; `birth_year`&#65311;"
test_object("birth_year", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#29992; `as.character()` &#23559;&#25976;&#20540;&#36681;&#25563;&#28858;&#23383;&#20803;&#65311;"
test_function("as.character",
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#23459;&#21578; `birth_year_char`&#65311;"
test_object("birth_year_char", 
            undefined_msg = msg, 
            incorrect_msg = msg)
            
sucess_msg("&#22826;&#26834;&#20102;&#65292;&#25105;&#20497;&#22312;&#19979;&#19968;&#20491;&#32244;&#32722;&#23601;&#21487;&#20197;&#22823;&#21151;&#21578;&#25104;&#65292;&#36245;&#24555;&#20358;&#21543;&#65281;")
```

--- type:NormalExercise lang:r xp:100 skills:4 key:a40e05d297
## 較難的衍生變數（3）

呼，終於要完成這個有點麻煩的衍生變數了！我們接下來要將剛剛生成的 `birth_year_char` 與 `birthday` 結合，字串的結合我們要使用 [paste()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/paste) 函數：

```{r}
char_pasted <- paste(char1, char2, sep = " ")
```

注意預設的 `sep = ` 參數是空格，由於西元日期會以 `-` 連接，所以記得要使用 `sep = "-"`。結合好以後我們只需使用 [as.Date()](http://www.rdocumentation.org/packages/base/versions/3.3.1/topics/as.Date) 函數將字元轉換成**日期**格式，就可以將這個向量新增至資料框了！

*** =instructions
```{r}
- 使用 `paste()` 函數將 `birth_year_char` 與 `birthday` 結合起來，成為 `birth_date_char`。
- 使用 `as.Date()` 函數將 `birth_date_char` 轉成日期 `birth_date`。
- 將 `birth_date` 新增至資料框。
```

*** =hint
```{r}
- `paste()` 函數的參數記得要設為 `sep = "-"`。
- 鍵入 `straw_hat_df$birth_date <- birth_date` 就可以完成新增變數。
```

*** =pre_exercise_code
```{r}
straw_hat_df <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_1570/datasets/straw_hat_df.csv")
sys_date <- Sys.Date()
sys_date_year <- format(sys_date, '%Y')
sys_date_year_num <- as.numeric(sys_date_year)
age <- straw_hat_df$age
birthday <- straw_hat_df$birthday
birth_year <- sys_date_year_num - age
birth_year_char <- as.character(birth_year)
rm(sys_date)
rm(sys_date_year)
rm(sys_date_year_num)
rm(age)
rm(birth_year)
```

*** =sample_code
```{r}
# straw_hat_df 、 birthday 與 birth_year_char 已預先載入

# 結合 birth_year_char 與 birthday
birth_date_char <- 

# 將 birth_date_char 轉成日期 birth_date
birth_date <- 

# 將 birth_date 新增至資料框
straw_hat_df$birth_date <- 

```

*** =solution
```{r}
# straw_hat_df 、 birthday 與 birth_year_char 已預先載入

# 結合 birth_year_char 與 birthday
birth_date_char <- paste(birth_year_char, birthday, sep = "-")

# 將 birth_date_char 轉成日期 birth_date
birth_date <- as.Date(birth_date_char)

# 將 birth_date 新增至資料框
straw_hat_df$birth_date <- birth_date
```

*** =sct
```{r}
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `paste()` &#20989;&#25976;&#65311;"
test_function("paste",
              args = c("x", "sep")
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `paste()` &#20989;&#25976;&#29983;&#25104; `birth_date_char`&#65311;"
test_object("birth_date_char", 
            undefined_msg = msg, 
            incorrect_msg = msg)
            
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#27491;&#30906;&#20351;&#29992; `as.Date()` &#20989;&#25976;&#65311;"
test_function("as.Date",
              not_called_msg = msg,
              args_not_specified_msg = msg,
              incorrect_msg = msg)
              
msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#20351;&#29992; `as.Date()` &#20989;&#25976;&#29983;&#25104; `birth_date`&#65311;"
test_object("birth_date", 
            undefined_msg = msg, 
            incorrect_msg = msg)

msg = "&#30906;&#35469;&#26159;&#21542;&#26377;&#25104;&#21151;&#23559; `birth_date` &#26032;&#22686;&#33267;&#33609;&#24125;&#28023;&#36042;&#22296;&#36039;&#26009;&#26694;&#20013;&#65311;"
test_object("straw_hat_df$birth_date", 
            undefined_msg = msg, 
            incorrect_msg = msg)

success_msg("&#33021;&#22816;&#23436;&#25104;&#36889;&#20491;&#31995;&#21015;&#30340;&#32244;&#32722;&#20320;&#30495;&#30340;&#26159;&#22826;&#19981;&#31777;&#21934;&#20102;&#65292;&#30475;&#20358;&#20320;&#24456;&#26377;&#28507;&#21147;&#25104;&#28858;&#33609;&#24125;&#28023;&#36042;&#22296;&#30340;&#31532;&#21313;&#20491;&#22821;&#20276;&#65281;")
```