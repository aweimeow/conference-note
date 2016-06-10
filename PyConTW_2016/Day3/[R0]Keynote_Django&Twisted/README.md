# PyCon TW 2016 Collaborative Notes <br> Keynote - Amber Brown

> ### Quick Links
> - [Portal for Collobration Notes 共筆統整入口](https://hackfoldr.org/pycontw2016) (hosted by [hackfoldr](https://hackfoldr.org/about) and [HackMD](https://hackmd.io/))
> - [Program Schedule 議程時間表](https://tw.pycon.org/2016/events/talks/)
> - [PyCon TW 2016 Official Site 官網](https://tw.pycon.org/2016/)
>
> ### How to update this note?
> - Everyone can *freely* update this note. 任何人都能自由地更新內容。
> - Please respect all the participants and follow our [code of conduct](https://tw.pycon.org/2016/about/code-of-conduct/) during discussion. 討論、記錄時，請遵守大會的[行為準則](https://tw.pycon.org/2016/about/code-of-conduct/)

## "Django & Twisted"

### Abstract

Web frameworks like Django are designed around the traditional request-response cycle — a request comes in, a response is generated, and that is delivered to the client. In the day of “single page” applications, where only sections of the page are updated through requests, doing real-time can be clunky. Twisted, and things that build off it, like Django Channels, might be the way forward. What problems does this fix? How does this make the user experience better? What new issues arise when you're doing everything asynchronously? And how will this change in the future? are all topics we'll get in to. 

#### Scaling Django Application
> Django server only response one request a time

concurrent request = thread x pools

Higher scale means higher complexity

有沒有更好的方法去容納更多的 request ?

CPU-bound: 數學運算、資料運算等
IO-bound: Database requests, web requests, other network IO
ex. 跟資料庫溝通獲取某些資訊


#### Asynchronous IO Programming
所有的事件都是從 IO 來的，我們就等他來就好啦 ~

### Twist

#### selector function
有一個 list 有一堆 file descriptor（socket, ...）
selector loop 可以處理上千個 file descriptor (?)
nothing locks, it give control to the next event
no blocking means no threads

event driven 的最佳case是I/O bound的程式，低CPU使用率

若程式是CPU bound，則搭配task queue

Putting task on the queue and removing them is cheap
所以 task queue 要擴張比較容易
想要做更多工作的話，就增加更多的 worker 吧


### Django channel

Project for  Asynchronous django

> interface server > channel queue > many of workers

interface server: 就只是接收 requests
workers: 拿走 queue 裡面的 request 然後處理他們，處理完後在放回 channel

當 requests 被 worker 處理好的時候 
interface server 會把 response 撿走
拿去回應到對的 requests

[daphne](https://pypi.python.org/pypi/daphne): Daphne is a HTTP, HTTP2 and WebSocket protocol server for ASGI, and developed to power Django Channels.
Daphne is written in Twisted.

> The channel layer can be shard ( ?
> 可以有很多個 channel queue 一起處理這些 request

worker 也不一定要被放在 web server 裡面
如果規模不大的話，也可以把 channel queue 放在 shared memory 裡面


### how channels work

request
- incoming HTTP request

workers listen on these channel name（如果有工作就送給 worker）
```
http.response!c134x7y
有這個 code 就能把他指回去對的地方
```

worker 自己預設不會使用非同步 IO，你不會有 blocked worker 這種東西

#### group


worker can listening on specific channel, they don't need to listen all of them

fan-out message


#### Channel is a bridge to  Asynchronous feature
[Django Channel document](http://channels.readthedocs.io/en/latest/)

可能在 Django 1.11/2.0 會 release

### QA Time

* Q: Why JSON not BSON...?
* A: 在一般狀況下 JSON 足以，但在需要的情況下， 可以自訂需要的 serialization(非官方)

* Q: queue 是 FIFO，可以自訂嗎？
* A: 在 Channel 這層只能 FIFO, 如果需要針對不同的 task 有不同的處理優先權, 可以把不同種類的 tasks 放到不同的 channel 上, 就能用個別的 worker 去處理

* Q: in-memory queue?
* A: 需要 IPC，很多 machine 的情況下沒辦法 (?) 

