### Работа с файлами

```go
package main

import 	"os"

func main() {
	// Создание файла
	newFile, err := os.Create("test.txt")
	if err != nil {
		println("Something went wrong")
		return
	}
	
	_ = newFile.Close()
	
	// Усечение файла до 100 байт
	err = os.Truncate("test.txt", 100)
	if err != nil {
		println("Something went wrong")
		return
	}
	
	// Получение информации о файле
	var fileInfo os.FileInfo
	fileInfo, err = os.Stat("test.txt")
	if err != nil {
		println("Something went wrong")
	}
	println("File name:", fileInfo.Name())
	println("Size in bytes:", fileInfo.Size())
	println("Permissions:", fileInfo.Mode())
	println("Last modified:", fileInfo.ModTime())
	println("Is Directory: ", fileInfo.IsDir())
	
	// Переименование файла
	err = os.Rename("test.txt", "test2.txt")
	if err != nil {
		println("Something went wrong")
	}
	
	// Удаление файла
	err = os.Remove("test2.txt")
	if err != nil {
		println("Something went wrong")
	}
}
```

Открытие файла только на чтение

```go
package main

import "os"

func main() {
	// Простое открытие на чтение
    file, err := os.Open("test.txt")
    if err != nil {
        println("Something went wrong")
        return
    }
    
    file.Close()
}
```

Открытие файла для модификации

```go
package main

import "os"

func main() {
	// Простое открытие на чтение
    file, err := os.OpenFile("test.txt", os.O_APPEND, 0666)
    if err != nil {
        println("Something went wrong")
        return
    }
    
    file.Close()
}
```

Запись в файл

```go
package main

import "os"

func main()  {
    // Создать файл только для записи
    file, err := os.OpenFile(
        "test.txt",
        os.O_WRONLY|os.O_TRUNC|os.O_CREATE,
        0666,
    )
    if err != nil {
        println("Something went wrong")
        return
    }
    
    defer file.Close()
    
    // Пишем в файл
    byteSlice := []byte("Bytes!\n")
    bytesWritten, err := file.Write(byteSlice)
    if err != nil {
        println("Something went wrong")
        return
    }
    println("Bytes written:", bytesWritten)
}
```

Построчное/пословное чтение

```go
package main

import (
	"os"
	"bufio"
)

func main() {
	file, err := os.Open("test.txt")
	if err != nil {
        println("Something went wrong")
        return
	}
	
	defer file.Close()
	
	scanner := bufio.NewScanner(file)
    
    // По умолчанию читает построчно 
    // Но мы настроим на чтение по словам
    scanner.Split(bufio.ScanWords)
    
    success := scanner.Scan() 
    if success == false {
        err = scanner.Err()
        if err == nil {
            println("Scan completed and reached EOF")
        } else {
            println("Something went wrong")
        }
        return
    }
    
    println("First word found:", scanner.Text())
}
```