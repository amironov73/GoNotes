### Отражение (reflection)

В Go предусмотрен механизм отражения, и он вполне функционален, хотя, после .NET кажется немного куцым. В Go есть даже атрибуты, но после C# они откровенно разочаровывают. Впрочем, жить со всем этим можно. Также можно надеяться на лучшее, возможно, в будущем это всё доработают.

API отражения проживает в стандартном пакете reflection, он довольно прост и интуитивно понятен:

```go
package main

import "reflect"

type Person struct {
	Name    string `json:"name"`
	Address string
	Age     int `json:"age"`
}

func main() {
	person := Person{}
	t := reflect.TypeOf(person)
	for i := 0; i < t.NumField(); i++ {
		field := t.Field(i)
		name := field.Name
		json := name
		if j, ok := field.Tag.Lookup("json"); ok {
			json = j
		}
		println(field.Name, "->", json)
	}
}
```

Программа выведет

```
Name -> name
Address -> Address
Age -> age
```