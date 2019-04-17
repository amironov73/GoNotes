### Слайсы

Самый волнующий вопрос: как удалить элемент из середины слайса? А вот как:

```go
func removeAt(s []int, i int) []int {
    edge := len(s) - 1
    s[i] = s[edge]
    return s[:edge]
}
 
// Удаление с сохранением порядка элементов:
 
func removeOrdered(a []int, i int) []int {
    return a[:i+copy(a[i:], a[i+1:])]
}

```

Вставка элемента в середину слайса:

```go
func insertAt(s []int, i, v int) []int {
    s = append(s, 0)
    copy(s[i+1:], s[i:])
    s[i] = v
    return s
}
 
// Вставка нескольких элементов в середину слайса:
 
func insertMany(s []int, i int, v []int) []int {
    return append(s[:i], append(v, s[i:]...)...)
}
```

Извлечение первого элемента из слайса:

```go
func shift(s []int) (int, []int) {
    return s[0], s[1:]
}
```