# Talk: Reactive Programming in Python

- Info: https://tw.pycon.org/2016/events/talk/67738180727603248/
- Slides: https://speakerdeck.com/keitheis/reactive-programming-in-python
- Speaker: Keith Yang

#### What is reactive programming
>game is reactive.

- Programming PARADIGMS
	- Declarative
	  Function language: Scheme, Clojure, Erlang, Haskell, OCaml
	- Imperative
	  Procedural programming language: C, Go, Fortran, Pascal, Basic

#### 事前預習

###### Map
Map a iterable, a list, into a function
```python
>>> str_map = map(str, [1, 2, 3])
>>> list(str_map)
['1', '2', '3']
```

###### Lambda
Create small annoymous function inline
```python
>>> multiple_7 = lambda x: x * 7
>>> type(multiple_7)
function

>>> multiple_7(6)
42
```

###### Map & Lambda 組合技
```python
>>> list(map(lambda x: x * 2, [1, 2, 3]))
[2, 4, 6]
```

#### Stream
> Everything can be a stream

##### Stream in `for in if`
* list comprehension
* generator expression

```python
from pathlib import Path
from zipfile import ZipFile

file_stream = (
	ZipFile(file.name)
	for file in Path(".").iterdir()
	if file.name.lower().endswith('.zip')
)

zipped_content_list = []
for a_zipfile in files_stream:
	for item_name in a_zipfile.namelist():
		zipped_content_list.append(item_name)
```

* in reactive style
```python
from pathlib import Path
from zipfile import ZipFile
from functional import seq

zipped_content_list = (
	seq(Path(".").iterdir())
	.filter(lambda item: item.is_file())
	.filter(
		lambda file: file.name.lower().endswith('.zip')
	).map(ZipFile)
	.flat_map(lambda a_zipfile: a_zipfile.namelist())
)
```

#### Why reactive programming
- Abstraction
- Focus on Business logic
- Concise code
- Performance
	- Usually seen in `asynchronous` context
	- Parallel processing, small unit of change

#### PyFunctional
```python
from functional import req

def is_even(num):
	return (num % 2) == 0

evens3 = seq(num_stream).filter(is_even)
# [2, 4, 6]
```
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