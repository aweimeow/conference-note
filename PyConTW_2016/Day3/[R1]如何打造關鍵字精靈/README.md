## Talk: 如何打造關鍵字精靈
- Info: https://tw.pycon.org/2016/en-us/events/talk/57694625669840919/
- Slider: http://www.slideshare.net/ssuser05afc89/how-to-build-an-keyword-wizard
- Speaker: 施晨揚


#### What is keyword
是一個有指標或是有識別性的字詞，且他也包含著一些特定的意義

#### Why we need ?
- Advertisement (廣告)
- TAG (標籤)
- Relation (關聯性)
- Article Summary (文章的總結)

#### Word Relation Model
關聯性搜尋
* Model 1（關聯詞)
沖繩 -> 飯店、自由行、推薦
* Model 2（同義詞）
沖繩 -> 琉球、壺屋通、...

#### Word Representation - Vector Space Model
把文字、文章 Mapping 到多維向量空間
可以看出那些文章，或是哪些詞是有關係的

#### One Hot v.s Continue Value 
如果是維度十分高的話（多維空間），是很難辨識出哪些詞是相似的

#### Word Representation  -One Hot Representation
最簡單的方法 - One Hot Representation
先把每一個詞建出一個 `One Hot Index`
但是這種編碼模式會找不到詞與詞之間的相關性，找關係會很難找

#### Word Representation - Context Vector
在範例中，以詞作為 X Y 軸來產生一個表格，
把兩個詞之間同時出現的機率來辨識出兩個詞之間的相關性
Ex. 沖繩 vs. 浮淺 = 0.7, 沖繩 vs. 餐廳 = 0.1

#### Word Context Vector
講到拉麵 -> 美味しい
講到一蘭 -> 喔依西捏
就可以把兩個詞關聯起來

> 可是一蘭和赤坂明明都不好吃啊
> 別醬子 XD

#### Co-occurrence Matrix
如果很大的話 n ~= 500k
那 space = n & n，time = n *n 

#### Word2Vec

word2vec = 兩層式的類神經網路
「我想要去沖繩 ... 潛水」必須再看到前面的字就要能預測出會說 `潛水`，
可能的詞有：打球、潛水、睡覺、...、洗臉（可能有好多個 Label），

可以用類神經網路來逼近出這個 Model，

[Reference](https://www.tensorflow.org/versions/r0.8/tutorials/word2vec/index.html)

#### Major Process Flow

1. Article Selection
2. Content Extraction
3. Word Cutting
 

#### Article Raw Data Preparation

文章都是一行，要幫文章做斷詞，把文章中的詞以空格隔開。


#### Term Database
收集詞庫
- Search Log
- 各大電商網站(e.q 阿里巴巴)
	- Link1
	- Link2
- http://baseterm.com/
- 輸入法詞庫
	- 詞庫 破解
	
#### Term Database - Search Log
`google search sole` → `search histroy` →`Filter & Counting` →`Term Collection`

#### Search Log
從 search log 產生詞庫，可以直接用 count 來做，
累積到一定的數量，就可以知道 `太陽的後裔` 是一個新詞
但是可能會有奇怪的詞混進來，所以要限制長度

#### Term Database

#### Word Cutting

- Word Cut Tool
	- Jieba 
- Get Bot Token

> 推結巴，好用