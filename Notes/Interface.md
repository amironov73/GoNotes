### Интерфейс

#### Как сконвертировать слайс структур в слайс интерфейсов

Простым кастом превратить слайс структур в слайс интерфейсов нельзя -- компилятор упорно отказывается, мотивируя тем, что такие слайсы по-разному расположены в памяти.

Остаётся единственный выход -- конвертировать вручную поэлементно.

```go
func convert(dataSlice []T) []interface{} {
    result: = make([]interface{}, len(dataSlice))
    for i, d := range dataSlice {
	    interfaceSlice[i] = d
    }
    return result
}

var dataSlice []int = foo()
bar(convert(dataSlice))
```