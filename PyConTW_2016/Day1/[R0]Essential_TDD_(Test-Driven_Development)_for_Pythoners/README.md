## 共筆

- Info: https://tw.pycon.org/2016/events/talk/70169571679535177/
- Speaker: 曾君宇 [均一教育徵才中](http://www.junyiacademy.org/)
- Slides: http://www.slideshare.net/excusemejoe/essential-tdd-pycontw2016
- TDD (Test-Driven Development)
	- Red, green, refactor cycle
	- 預想好使用情境
	- 一次只會專注一個目標，一次解決一個問題
	- 避免過度設計
- 其他 *DD
	- ATDD(驗收測試驅動開發)：
		- 聚焦在客戶的需求
		- 按照spec做開發
	- BDD
- TDD的八卦？！
	- 2014就掛惹！ by Rails創作者
	- [懶人包：TDD is Dead 戰文總整理 ](http://joe-dev.blogspot.tw/2014/06/tdd-is-dead.html)
		- PyCon結束再看 ^.< (不然PyCon就結束了)
- 結論？
Mindset：設計決策一次只聚焦在一個地方
好好評估環境適不適合TDD（連需求都不確定時，不建議使用TDD）

推薦書籍：[Test-Driven Development with Python](http://chimera.labs.oreilly.com/books/1234000000754) (O'RELLY)

## 會後延伸閱讀筆記整理

#### Test Driven Development 重點翻譯
Link: [http://www.martinfowler.com/bliki/TestDrivenDevelopment.html](http://www.martinfowler.com/bliki/TestDrivenDevelopment.html)

> TDD 是被 [Kent Benk](https://twitter.com/KentBeck) 開發用來作為 Extreme Programming 的一部分

主要只有三個步驟：
1. 為你下一塊要實作的功能寫一段測試(test)
2. 開始開發要實作的功能，直到寫的測試都能夠通過
3. 重構程式碼，讓其架構清晰明瞭

持續重複這三個步驟，一次一個測試，一步一步地建立起整個系統，
這種先寫測試的步驟，被 [XPE2](http://www.amazon.com/Extreme-Programming-Explained-Embrace-Change/dp/0321278658?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321278658&linkCode=as2&redirect=true&tag=martinfowlerc-20) 稱作 `Test-First Programming`  

這種做法有兩個好處：
1. 你可以只寫部分程式去為了使測試通過
2. 為了使測試通過，你會去構思 code 的介面怎麼樣是比較好的

這樣子會使你專注於介面上，把介面與實作從 class 抽離開

其實聽到有人搞砸 TDD 是因為忽略了第 3 個步驟，  
`重構程式碼`能保持程式碼的整潔，否則程式碼會很凌亂，
不過就算凌亂，這些 code 也是被測試過了，至少以結果上而言，不會比錯誤的設計還痛苦。


#### Self Testing Code 重點翻譯
Link: [http://www.martinfowler.com/bliki/SelfTestingCode.html](http://www.martinfowler.com/bliki/SelfTestingCode.html)  

Self-Testing Code 是指在軟體中與軟體相關的複雜的自動測試，
當完成的時候，可以用一條指令完成所有測試，
而且，這些測試讓你有十足的信心能發現隱藏在程式裡面的 bug

這個想法是來自於一場會議，
「如果能夠下一條指令，然後整個系統就自己測試完」
這個想法就像是你除了在打造軟體之外，同時也在完成能夠檢查任何錯誤的 bug detector，

自動化測試也是 `持續整合` 的關鍵部分，
換句話說，如果你沒有自動化測試，那就不是真正的 [Continuous integration](http://www.martinfowler.com/articles/continuousIntegration.html)，
而自動化測試也是 [Continuous Delivery](http://www.martinfowler.com/delivery.html) 的一部分。

自動化測試的一個好處就是可以大量減少 bugs 發生的數量，
但是最大的好處並不是避免製造出 bugs，
而是當你作任何更動的時候，你會對自己的軟體有信心。

在自動化測試中，團隊會有一個很重要的行為，就是實際用自動化測試去引發 bug，
通常一個團隊都是寫測試去找到 bug，然後就試著去修補這個 bug，
在寫測試的時候，常常會是一連串的測試，接著把測試切細到[單元測試](http://www.martinfowler.com/bliki/UnitTest.html)

