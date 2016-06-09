# Talk: Boost Maintainability

- Info: https://tw.pycon.org/2016/events/talk/58446570282024986/
- Speaker: Mosky Liu
- 投影片: https://speakerdeck.com/mosky/boost-maintainbility


我們在開發程式的時候，都是 "read lines randomly" 的，不像電腦會逐行讀取。

> [Making wrong code look wrong](http://www.joelonsoftware.com/articles/Wrong.html) - Joel on software

#### Maintainability
用人讀 code 的方式來定義 Maintainability
> To understand a random line, the lines you need to read back.

相對於programmer的時間，運算資源比較不值錢。
把時間專注於想要做的事情，而不是 debug 上面。

#### Boost Maintainability
- Define our "Maintainability"
- Making it zero
- progressive from zero

##### Maintainability
Be exact & consistent (命名要精準且有一致性)

##### 舉個例子
```python
result = ...
result = ...
```
以這種方式來命名不夠準確所以很容易混亂

##### 命名的好方法
常常用 dictionary，對一個領域不熟悉的話可以多查字典來找到更好的名字哦！

#### Ops Hint
命名具有提示的作用，提示有怎樣的operation可以用
```python
page_no = ...
page_html = ...
```
這樣就可以知道 `page_no` 是一個數字，而 `page_html` 是一個字串

```python
allowed_field_set = set(requested_field)
```
這樣能清楚知道他是一個集合(set)

##### consistent問題
用d來標示dictionary
```python
user = User(...)
user_d = {}
```

>Hint: func 的命名如果沒有取名好，那發現問題還需要查 document，這個更耗時
建議：func都用動詞開頭，就會記得加上()


不要把 `is_secure = True` 與 `req.is_secure()` 混用
以 `形容詞`、`介係詞` 來當 boolean 會比較好
或者用簡單的句子來表示 boolean: `req_is_secure = True`

#### Ops Hint (Mosky 使用的習慣)
- Hint which ops you should use
- _no: numeric
-  <plural>: sequence, usually is mutable sequence(list).
-  _<type>: if no intuitive way
-  (這邊好像有缺漏，求有筆記到的幫補充)
- <verb>_: imperative sentence
- <yes-no question>: return boolean
- to_<thing>: thing
- boolean: <adj>, <prep>, <simple sentence>

##### return value
- get_page_no -> numeric >= 1
- query_user -> user object
- parse_to_tree -> tree object

##### avoid `None`
Consider:
```python=
user = query_user(uid)
user.is_valid()
```
如果查不到 user 就 ret None 的話，就會噴 Error 囉！

Accept an exception ?
- N: user dummy object like an empty string.
- Y: just raise when you wanna assign to None.


#### 如果沒有檢查好做好處理
```python=
tmpl = '<p>{}</p>'.format(name)
name = '<script> ... </script>'
#XSS
```
```python=
tmpl_html = ... .format(
	escape_to_html(name)
)
```
這種不是 python 的東西，對 Python 而言就只是 str，所以要去處理

#### Structure Hint

```python=
uid_email_map = {
	'mosky': 'mosky@email'
}
```
這樣子的命名方式能夠更直覺

##### for dict & tuple
- <key>_<value>_map
- tuple
	- _pair: 2-tuple
	- _pairs: 3-tuple


#### Private Hint

- _<name>
- Dont use out of class, function


#### Performance Hint
- get: memory op (記憶體的操作)
- parse_ / cale_: CPU-bound op
- query_ : IO-bound op
- query_or_get_: IO-bound op with cache


#### Progressive from zero
- 不要自己自創縮寫，可以去[網站](http://www.abbreviations.com/)上查
- 如果只是要在一個 func 裡面用而已，可以用註解來解釋縮寫定義
（目前著重於讓人能夠更快讀懂 code，所以才這樣說）
- 把程式分段跟分節
	- 把做一系列事情的分段及分節
	- 用 `空行` 來把不同的事情分隔開
	- 用 `section` 的方式來切開（Title comment 來區隔開不同的區塊）


#### Line Function up（把程式連線起來）
> Func A call Func U, Func B call Func U

可以從連線的方式來慢慢切開變成函式的模組化
>Hint: 最好把箭頭指向的方向全統一到同個方向


#### Face Bad Smell（察覺程式碼中的壞東西）
>不要為了克服心理上的潔癖而造成開發上時間的損失
>就是不要因為覺得 code 很醜就浪費一下午改好又不能動 XD

- 用 comment 來解決痛點而不是改寫
- 放很多 TODO，不是不改是時候未到 XD
- Seal it：把他封起來就對了，或是用更好的名稱把他包起來
	- def good_name(): bad_name()
- Stay focused：認真寫 code，舊的東西先放著！

#### Summary
> Use hints to boost maintainability !


#### QA

1、如何影響同事在 co-working 上使用較好的命名？

絕對不要有 guild line，可是可以用 `I will prefer` 這種方式來慢慢改變同事的風格，當他們發現這麼做的好處就會漸漸跟著改變。
但是真的碰到沒有按照規則走的同事也不要太生氣，可以 comment 他（幫他補一堆 comment），幫他 wrapper，然後讓自己的工作更順利。

2、你會參考 google 的 programming guildline 嗎？

會參考唷！