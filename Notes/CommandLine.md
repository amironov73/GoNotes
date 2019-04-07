### Работа с параметрами командной строки

В стандартной библиотеке Go предусмотрен пакет для работы с параметрами командной строки приложения. Называется он довольно неожиданно: flag, так программист может спокойно пройти мимо. Зато API у него простой и понятный:

```go
package main
 
import (
    "flag"
    "fmt"
)
 
var (
    input = flag.String("in", "input.txt", "Name of the input file")
    output = flag.String("out", "output.txt", "Name of the output file")
    blockSize = flag.Int("size", 4096, "Size of the block")
)
 
func main()  {
	// Приказываем пакету разобрать командную строку
	flag.Parse()
	
    fmt.Println("Input file:", *input)
    fmt.Println("Output file:", *output)
    fmt.Println("Block size:", *blockSize)
    // делаем что-нибудь с указанными файлами
}
```

Теперь запустим программу из командной строки:
```
experiment -in Source.txt -out Target.txt -size 100500
```

Она напечатает:

```
Input file: Source.txt
Output file: Target.txt
Block size: 100500
```

Если не указать в командной строке какой-либо параметр, он примет значение по умолчанию. Всё просто, не так ли?
