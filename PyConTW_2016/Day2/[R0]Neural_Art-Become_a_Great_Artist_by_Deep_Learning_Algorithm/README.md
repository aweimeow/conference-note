## Talk: Neural Art -- Become a Great Artist by Deep Learning Algorithm
- Info: https://tw.pycon.org/2016/events/talk/27429730160476163/
- Speaker: Mark Chang
- Slides: http://www.slideshare.net/ckmarkohchang/neural-art-english-version
- Source Code of Neural Art: https://github.com/ckmarkoh/neuralart_tensorflow

#### 人類藝術家是怎麼畫畫的
論文: [A Neural Algorithm of Artistic Style](http://arxiv.org/pdf/1508.06576v2.pdf)
1. 看到畫面然後變成訊號
2. 混上自己的風格特色
3. 畫出來

#### Visual Perception
- 最小的單元 - Neuron 神經元
- Neuron 結合起來形成 visual pathway

#### Visual Pathway
- 視網膜接收到的訊號會透過相互連接的神經元所形成的 visual pathway 傳送到 visual area

##### Visual Area V1
這個部分只會感覺到線條

##### Visual Area V4
這個部分能夠認知方形、三角形、圓形等幾何圖形

##### Inferior Temporal Gyrus
這可以認知到更複雜的圖像

#### Misconception 錯覺
是這個演算法能成功很重要的一個環節

在例子當中，有兩個相同顏色的灰點，如果我們幫他們加上不同顏色的背景，那他們的顏色看起來就會不同。
如果有兩條平行的線，幫他加上同心圓，那看起來就會變得扭曲
如果有兩條一樣長的線，幫他們加上不同角度的兩側就會看起來不一樣長

> "misconception"?? <-- does he mean "false perception" or "illusion"??
> not sure about the differences between them
> "misconception" = "誤解"

#### Computer Vision
- Neural Networks
X: input signals
w: weight of each input signals
n: linear combination of input signals

Sigmoid, Rectified Linear Function (non-linear function)

sigmoid: 如果 input 趨近於零，那輸出就會是 0
Rectified Linear: 如果輸入小於 0，那輸出就會是零，如果大於零，則保持原輸出

> input layer > hidden layer > output layer

#### Convolutional Neural Networks
responsible for visual signals
duplicate neuron with same weight in different position to sense the color, shape, ...


- stride
- padding
- pooling: maximum/average pooling

> Input layer > Convolutional layer > Pooling > ??? > Pooling > Output layer
在 Convolutional layer ，會辨識出線，在 Pooling ... 等三層，可以辨識出方形、圓形等形狀


#### VGG 19 (Convolutional Layer)
[Very deep convolutional networks for large-scale image recognition](https://arxiv.org/pdf/1409.1556.pdf)

這個演算法在 ImageNet 2014 獲得冠軍的獎項
他有 19 + 5 個層
 
pre-trained parameter can be downloaded online
不用再自己訓練資料，訓練資料十分耗時


#### Neural Art
模仿人類藝術家畫畫
人類藝術家看到 101 -> 腦海生成畫面(不是真的 101，只是訊號，因為有錯覺，所以他不知道真實的樣子，只知道大概的樣子) -> 只能盡量把畫出來的和真實畫像的差異降低。

VGG 19 是一個商業化軟體，有很高的精確度去辨識出圖像來

第一層會記錄下 location，

##### Content Generation
Input Photo P、Input Canvas x 各自丟入VGG19再minimize兩者的差利用backpropogation修正canvas的RGB value
higher layer會讓圖的細節loss越多，因為neural network是模仿人類的visual path
你可以看到一次又一次的，畫出來的畫像和真實的照片越來越相近

##### Style Generation
"Style" is position-independent --> Gram Matrix


我們把有風格的圖畫餵給 VGG19，把他轉換成 Gram Matrix，產生出 Style Image

在第一層，我們只能看到有細碎的風格，隨著層數往後，我們能更清楚的看到風格的細節


##### Artwork Generation

Content vs Style
在創造結果時，我們不要原圖的細節，所以我們只取較後面的層，
在抽畫風的時候則要保留細節，可以把layer疊在一起

Initial State 對於最後的結果也有很重要的影響，
如果完全沒有對於產生的圖像有任何提示的話，那會和風格輸入的圖片很相近，如果有一些提示（大樓的陰影等），那就會和我們要的結果比較相近，如果把台北 101 的照片餵進去作為 Initial State 的話，那產生出來的就會是最精確的有畫作風格的圖片。


#### Recurrent Neural Network (RNN)
language model for generating poet