### Пакет bufio

Стандартный пакет bufio реализует буферизованный ввод/вывод. Он оборачивает объект io.Reader или io.Writer, создавая другой объект (Reader или Writer), который также реализует интерфейс, но обеспечивает буферизацию и некоторую поддержку для текстового ввода-вывода. В общем, ничего необычного.

Пример: читаем стандартный ввод построчно.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	scanner := bufio.NewScanner(os.Stdin)
	for scanner.Scan() {
		fmt.Println(scanner.Text()) // Println will add back the final '\n'
	}
	if err := scanner.Err(); err != nil {
		fmt.Fprintln(os.Stderr, "reading standard input:", err)
	}
}
```

Ещё пример: читаем строку по словам, разделенным пробелами.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

func main() {
	const input = "Now is the winter of our discontent,\nMade glorious summer by this sun of York.\n"
	scanner := bufio.NewScanner(strings.NewReader(input))
	scanner.Split(bufio.ScanWords)
	count := 0
	for scanner.Scan() {
		count++
	}
	if err := scanner.Err(); err != nil {
		fmt.Fprintln(os.Stderr, "reading input:", err)
	}
	fmt.Printf("%d\n", count)
}
```

Ещё пример: буферизованный вывод.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	w := bufio.NewWriter(os.Stdout)
	fmt.Fprint(w, "Hello, ")
	fmt.Fprint(w, "world!")
	w.Flush() // Не забываем!
}
```
