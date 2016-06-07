# Talk: Reactive Programming in Python

- Info: https://tw.pycon.org/2016/events/talk/67738180727603248/
- Slides: https://speakerdeck.com/keitheis/reactive-programming-in-python
- Speaker: Keith Yang

#### What is reactive programming
>game is reactive.

- Programming PARADIGMS
	- Declarative
	- Imperative

#### Stream
> Everything can be a stream

##### Stream in `for in if`
* list comprehension
* generator expression

> 眼睛會痛XD

#### Why reactive programming
- Abstraction
- Focus on Business logic
- Concise code
- Performance
- asynchronous programming

#### PyFunctional
- `from functional import seq`
> core spirit: Stream

[most.js](https://github.com/cujojs/most): Monadic reactive streams

[Python reactive extension](https://github.com/ReactiveX/RxPY)
Handle for you: 
- Thread-safty
- Syncronization
- etc ...
 
Implementation:
- RxPy
- RxJava
- RxCpp
- etc ...

> Asynchronous programming is HARD.


### RxPy

#### Observable



#### flat_map

複雜的 list 的扁平化（我要的值在 list 的每個event中）

```python
str_ls = [['6', '7'], ['42']]
```

### books
* Python Reactive Programming
* Reactive Programming with Scala and Akka
* Reactive Programing with