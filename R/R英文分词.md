使用R语言进行分词，并进行简单分析

# 使用`tm`包词频统计

## 文本预处理

`tolower`函数将所有英文字母转换为小写字母，`removeNumbers`函数将数字删除，`removePunctuation`函数将标点符号删除，`removeWords`函数将停用词删除，`stripWhitespace`函数将多余的空格删除，`stemDocument`函数将单词还原为其词根。

## 词频统计

使用`TermDocumentMatrix`函数将语料库对象转换为文档-单词矩阵，然后使用`findFreqTerms`函数找出出现频率最高的单词，使用`rowSums`函数统计每个单词出现的总次数。

## 代码实现

将分词和词频统计两部分封装成函数`get_word_counts`，注意传入参数`text`为数据库的文本列，例如`tweets$text`

```R
library(tm)
get_word_counts <-function(text){
  # 分词
  corpus <- VCorpus(VectorSource(text))
  corpus <- tm_map(corpus, content_transformer(tolower))
  corpus <- tm_map(corpus, removeNumbers)
  corpus <- tm_map(corpus, removePunctuation)
  corpus <- tm_map(corpus, removeWords, stopwords("english"))
  corpus <- tm_map(corpus, stripWhitespace)
  corpus <- tm_map(corpus, stemDocument)
  # 统计词频
  tdm <- TermDocumentMatrix(corpus)
  freq_terms <- findFreqTerms(tdm, lowfreq = 50)
  word_counts <- rowSums(as.matrix(tdm))
  word_counts <- sort(word_counts, decreasing = TRUE)
  
  return(word_counts)
}
```

`demo`调用，[数据集链接](https://www.kaggle.com/datasets/euclidjie/tweets-text)

```R
tweets <- read.csv('tweets.csv')
word_counts <- get_word_counts(tweets$text)
# 输出词频前25单词
result <- data.frame(count = word_counts)
print(head(result, n = 25))
```



# 使用`wordcloud`绘制词云

```R
library(wordcloud)
# 获取前40个高频单词
top_words <- head(word_counts, n = 40)

# 绘制词云
wordcloud(words = names(top_words), freq = top_words, min.freq = 1, max.words = 100, random.order = FALSE, rot.per = 0.35, colors = brewer.pal(8, "Dark2"))
```

![image-20230305160110623](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202303051601690.png)