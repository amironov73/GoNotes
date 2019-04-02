### Кросс-компиляция

Скомпилировать исходный код для другой операционной системы очень легко. Под Windows

```
set GOOS=linux
set GOARCH=arm
go build hello.go
```

Под Unix:

```
GOOS=windows GOARCH=amd64 go build hello.go
```

#### Поддерживаемые значения GOOS

* aix 
* android 
* darwin 
* dragonfly 
* freebsd 
* hurd 
* js 
* linux 
* nacl 
* netbsd 
* openbsd 
* plan9 
* solaris 
* windows 
* zos

#### Поддерживаемые значения GOARCH

* 386 
* amd64 
* amd64p32 
* arm 
* armbe 
* arm64 
* arm64be 
* ppc64 
* ppc64le 
* mips 
* mipsle 
* mips64 
* mips64le 
* mips64p32 
* mips64p32le 
* ppc 
* riscv 
* riscv64 
* s390 
* s390x 
* sparc 
* sparc64 
* wasm

Естественно, не все сочетания GOOS/GOARCH поддерживаются. Вот перечень поддерживаемых:

* darwin/386
* darwin/amd64
* dragonfly/amd64
* freebsd/386
* freebsd/amd64
* freebsd/arm
* linux/386
* linux/amd64
* linux/arm
* linux/arm64
* linux/ppc64
* linux/ppc64le
* linux/mips
* linux/mipsle
* linux/mips64
* linux/mips64le
* linux/s390x
* nacl/386
* nacl/amd64p32
* nacl/arm
* netbsd/386
* netbsd/amd64
* netbsd/arm
* openbsd/386
* openbsd/amd64
* openbsd/arm
* plan9/386
* plan9/amd64
* plan9/arm
* solaris/amd64
* windows/386
* windows/amd64
