### Пакеты encoding/binary

Стандартный пакет «encoding/binary» в Go позволяет легко и просто считывать/записывать структуры из файлов/сокетов/любых других потоков. Работать с ним не просто, а очень просто:

```go
package main
 
import (
    "encoding/binary"
    "fmt"
    "io"
    "os"
)
 
type XrfRecord struct {
    LowPart  int32
    HighPart int32
    Status   int32
}
 
func ReadRecord(file *os.File, mfn int) *XrfRecord {
    offset := int64(mfn-1) * int64(12)
    _, err := file.Seek(offset, io.SeekStart)
    if err != nil {
        panic(err)
    }
    result := new(XrfRecord)
    // Здесь происходит магия
    err := binary.Read(file, binary.BigEndian, result)
    if err != nil {
        panic(err)
    }
    fmt.Println(result)
    return result
}
 
func main() {
    file, err := os.Open("ibis.xrf")
    if err != nil {
        panic(err)
    }
    defer func() { _ = file.Close() }()
 
    // считываем записи и делаем с ними что-нибудь
    ReadRecord(file, 1)
    ReadRecord(file, 10)
    ReadRecord(file, 100)
}
```

Запись в поток осуществляется аналогично функцией `binary.Write(w io.Writer, order ByteOrder, data interface{}) error`. 

Также можно читать/писать целые числа в нужном формате:

```go
package main

import (
	"encoding/binary"
	"fmt"
)

func main() {
	b := make([]byte, 4)
	binary.LittleEndian.PutUint16(b[0:], 0x03e8)
	binary.LittleEndian.PutUint16(b[2:], 0x07d0)
	fmt.Printf("% x\n", b)
}
```

Главное ограничение пакета — он работает только со структурами с полями фиксированной длины. Работает довольно быстро, хоть и через reflection.
