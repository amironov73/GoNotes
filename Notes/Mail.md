### Отправка почты

Для отправки почты через SMTP-сервер в Go можно использовать простой и эффективный пакет gomail. Его возможности:

* Аттачи;
* Встраивание картинок;
* Шаблоны HTML и плоский текст;
* Автоматическое кодирование спецсимволов;
* SSL и TLS;
* Отправка нескольких писем через одно подключение.

Документация здесь: https://godoc.org/gopkg.in/gomail.v2.

Пример программы:

```go
package main
 
import "github.com/go-gomail/gomail"
 
func main()  {
    m := gomail.NewMessage()
    m.SetHeader("From", "alex@example.com")
    m.SetHeader("To", "bob@example.com", "cora@example.com")
    m.SetAddressHeader("Cc", "dan@example.com", "Dan")
    m.SetHeader("Subject", "Hello!")
    m.SetBody("text/html", "Hello <b>Bob</b> and <i>Cora</i>!")
    m.Attach("/home/Alex/lolcat.jpg")
 
    d := gomail.NewDialer("smtp.example.com", 587, "user", "123456")
 
    // Send the email to Bob, Cora and Dan.
    if err := d.DialAndSend(m); err != nil {
        panic(err)
    }
}
```