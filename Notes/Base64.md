### Поддержка base64

За кодирование текст и структуры в base64 отвечает стандартный пакет, называющийся "encoding/base64" (правда, внезапно?). API у него простой и интуитивно понятный:

```go
package main

import (
	"encoding/base64"
	"fmt"
)

func main() {
	msg := "Hello, 世界"
	encoded := base64.StdEncoding.EncodeToString([]byte(msg))
	fmt.Println(encoded)
	decoded, err := base64.StdEncoding.DecodeString(encoded)
	if err != nil {
		fmt.Println("decode error:", err)
		return
	}
	fmt.Println(string(decoded))
}
```
