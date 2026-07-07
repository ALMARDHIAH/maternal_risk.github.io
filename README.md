# Data Science Project: Maternal Risk  2022
## About Project
The purpose of this project was to give students a deep understanding in examining large amounts of real-world data to uncover hidden patterns, generate insights, and direct decision-making. 
Our project was titled “Maternal Risk”, focused on two main objectives:
1.	Identify the maternal risk factors that cause high-risk pregnancy
2.	Identify the associations between maternal age and maternal risk

There were two types of analysis conducted in this project which were 
1.	data analysis (based on [maternal health risk data](https://www.kaggle.com/datasets/csafrit2/maternal-health-risk-data) 
2.	text analysis (based on text data).

## About Text Exploration
Text exploration has been conducted based on article titled “Challenges Facing during Pregnancy and Measures to Overcome” written by Gayatri Devi Ramalingam, Saravana Kumar Sampath and Jothi Priya Amirtham. This article explains the difficulties during pregnancy. The article can be accessed [here](https://www.intechopen.com/chapters/78926).

The purpose of conducting the text analysis was to get to know which topic or difficulty have been discussed the most in the article. The most frequent challenge dicussed would be considered as the main factor that cause high-risk pregnancy.

## R Studio Code
R code used to generate the wordcloud was as follow:
'''
install.packages("tm")
install.packages("SnowballC")
install.packages("wordcloud")
install.packages("RColorBrewer")

library("tm")
library("SnowballC")
library("wordcloud")
library("RColorBrewer")

text=readLines(file.choose())
docs=Corpus(VectorSource(text))
inspect(docs)

toSpace=content_transformer(function(x,pattern)gsub(pattern," ",x))
docs=tm_map(docs,toSpace,"/")
docs=tm_map(docs,toSpace,"@")
docs=tm_map(docs,toSpace,"\\|")
docs=tm_map(docs,content_transformer(tolower))
docs=tm_map(docs,removeNumbers)
docs=tm_map(docs,removeWords,stopwords("english"))
docs=tm_map(docs, removePunctuation)
docs=tm_map(docs, stripWhitespace)

docs=tm_map(docs, removeWords,c("can","women","pregnancy"))

dtm=TermDocumentMatrix(docs)
m=as.matrix(dtm)
v=sort(rowSums(m),decreasing=TRUE)
d=data.frame(word=names(v),freq=v)
head(d,100)

set.seed(1234)
wordcloud(words=d$word, freq=d$freq,
min.freq=1,max.words=200,random.order=FALSE,
rot.per=0.35,colors=brewer.pal(8,"Dark2"))

'''
##
