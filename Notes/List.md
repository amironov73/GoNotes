В стандартную библиотеку Go входит пакет "container/list", реализующий работу со связанными списками. Все необходимые операции (вставка в начало/конец, удаление, обход списка) реализованы. Пользуйтесь на здоровье!

```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	l := list.New()
	e4 := l.PushBack(4)
	e1 := l.PushFront(1)
	l.InsertBefore(3, e4)
	l.InsertAfter(2, e1)

	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}

}
```