---
title_meta  : 第一章
title       : 建立資料框
description : 一場爭奪 One Piece 的海上冒險！既然要學習資料框的分析技巧，我們得先在 R 語言的工作環境中建立出資料框才行，讓我們來複習一下在 [R 語言導論](https://www.datacamp.com/community/open-courses/r-%E8%AA%9E%E8%A8%80%E5%B0%8E%E8%AB%96#gs.kbSrfF8)中學過的內容吧！

--- type:NormalExercise lang:r xp:100 skills:1 key:9a073c3931
## 建立資料框

資料框的特性是可以在各個欄位容納不同的資料格式，在建立資料框之前，通常我們習慣先將各個欄位生成為向量，草帽海賊團主要角色設定有：

- 姓名
- 性別
- 職業
- 賞金
- 年齡
- 生日
- 身高

*** =instructions
- 使用 `data.frame()` 將右邊編輯區已經生成好的角色設定向量結合為一個資料框，並命名為 `straw_hat`。

*** =hint
- 在編輯區鍵入 `straw_hat <- data.frame(name, gender, occupation, bounty, age, birthday, height)`

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

```

*** =sample_code
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

*** =solution
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
