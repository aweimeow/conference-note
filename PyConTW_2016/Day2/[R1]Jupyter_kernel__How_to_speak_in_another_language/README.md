## Talk: Jupyter kernel: How to speak in another language
- Info: https://tw.pycon.org/2016/en-us/events/talk/56754637675429904/
- Slides: http://www.slideshare.net/AdrianLiaw/jupyter-kernel-how-to-speak-in-another-language
- Speaker:  廖偉涵 Adrian Liaw

#### agenda
1. Jupyter, IPython, notebook, console, clinet, kernel
2. The Interactive Computing Protocol
3. Implementing a kernet
4. Live Demo


#### Jupyter

> Client <- $\varnothing MQ$ Socket -> Kernel

- 也可以支援多個 client 連到相同的 Kernel 上面

#### What's inside IPython
- The interactive ipthon shell (No $\varnothing MQ$)
- Magic commands, ( e.g. ls, pwd, cd )
- Auto word completer
- beautiful traceback
- shell history management

[IPyKernel's repo](https://github.com/ipython/ipykernel)

#### What's inside jupyter
- web-based notebook interface & nbconvert


#### interactive computing protocol
>定義 kernel 和 client 要怎麼溝通
>有提供一些 pattern: request, reply, ...
- i.e. jupyter messaging protocol
- Communication between Kernel and Client
- Base on $\varnothing MQ$ and JSON

```sequence
Note left of Client: DEALER
Client->Kernel: SHELL
Note right of Kernel: ROUTER
Kernel->Client: SHELL
Note left of Client: DEALER

Note right of Kernel: PUB
Kernel->Client: IOPub
Note left of Client: SUB
Note right of Kernel: IOPub 會推\n執行的 Status

Note right of Kernel: ROUTER
Kernel->Client: stdin
Note left of Client: DEALER
Client->Kernel: stdin
Note right of Kernel: ROUTER

Note left of Client: DEALER
Client->Kernel: control
Note right of Kernel: ROUTER
Kernel->Client: control
Note left of Client: DEALER

Note left of Client: REQ
Client->Kernel: heartbeat
Note right of Kernel: REP
Kernel->Client: heartbeat
Note left of Client: REQ
```



[Jupyter 官方說明](http://jupyter-client.readthedocs.io/en/latest/api/client.html)

#### Kernel Types
- Native Kernel
- Python Wrapper Kernel
	- 在 IPyKernel 這個套件裡
- REPL Wrapper Kernel