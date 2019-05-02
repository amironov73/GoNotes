### Progress Bar

Библиотека [mpb](https://github.com/vbauerster/mpb) позволяет консольным приложениям на Go демонстрировать вполне профессиональные на вид прогресс-бары вроде такого (картинки заимствованы у автора, надеюсь он не против):

![mpb01](img/mpb01.svg)

или даже таких — комплексных:

![mpb02](img/mpb02.svg)

Возможности библиотеки:

* Можно отображать сразу несколько прогресс-баров;
* Динамический итог: возможность устанавливать значение total во время выполнения операции;
* Динамическое добавление/удаление прогресс-баров;
* Отмена операции;
* Заранее определенные декораторы: затраченное время, ожидаемое время выполнения, процент выполненной работы, счетчик байтов;
* Ширина декораторов у нескольких прогресс-баров автоматически синхронизируется.

Пример программы с прогресс-баром:

```go
package main

import (
    "math/rand"
    "time"

    "github.com/vbauerster/mpb/v4"
    "github.com/vbauerster/mpb/v4/decor"
)

func main() {
    // initialize progress container, with custom width
    p := mpb.New(mpb.WithWidth(64))

    total := 100
    name := "Single Bar:"
    // adding a single bar, which will inherit container's width
    bar := p.AddBar(int64(total),
        // set custom bar style, default one is "[=>-]"
        mpb.BarStyle("╢▌▌░╟"),
        mpb.PrependDecorators(
            // display our name with one space on the right
            decor.Name(name, decor.WC{W: len(name) + 1, C: decor.DidentRight}),
            // replace ETA decorator with "done" message, OnComplete event
            decor.OnComplete(
                // ETA decorator with ewma age of 60, and width reservation of 4
                decor.EwmaETA(decor.ET_STYLE_GO, 60, decor.WC{W: 4}), "done",
            ),
        ),
        mpb.AppendDecorators(decor.Percentage()),
    )
    // simulating some work
    max := 100 * time.Millisecond
    for i := 0; i < total; i++ {
        start := time.Now()
        time.Sleep(time.Duration(rand.Intn(10)+1) * max / 10)
        // ewma based decorators require work duration measurement
        bar.IncrBy(1, time.Since(start))
    }
    // wait for our bar to complete and flush
    p.Wait()
}
```
