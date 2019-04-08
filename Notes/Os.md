### Пакет os

Кроме обычных функций работы с файлами (Open, Close, Truncate), в пакете имеются также:

* **func Chdir(dir string) error** - смена текущей директории.
* **func Chmod(name string, mode FileMode) error** - смена атрибутов файла.
* **func Chown(name string, uid, gid int) error** - смена владельца файла.
* **func Chtimes(name string, atime time.Time, mtime time.Time) error** - перезапись моментов доступа к файлу.
* **func Clearenv()** - удаление всех переменных окружения.
* **func Environ() []string** - получение всех  переменных окружения.
* **func Executable() (string, error)** - получение пути к исполняемому файлу.
* **func Exit(code int)** - немедленное завершение программы. Отложенные функции не выполняются.
* **func Expand(s string, mapping func(string) string) string** - расширение фрагментов ${var} в строке. Приме:

```go
package main

import (
	"fmt"
	"os"
)

func mapper(placeholderName string) string {
	switch placeholderName {
	case "DAY_PART":
		return "morning"
	case "NAME":
		return "Gopher"
	}

	return ""
}

func main() {
	fmt.Println(os.Expand("Good ${DAY_PART}, $NAME!", mapper))

}
```

* **func ExpandEnv(s string) string** - расширение переменных среды в тексте.
* **func Getegid() int** - получение эффективного идентификатора группы для приложения.
* **func Getenv(key string) string** - получение значения переменной окружения.
* **func Geteuid() int** - получение эффективного идентификатора пользователя для приложения.
* **func Getgid() int** - получение идентификатора группы для приложения.
* **func Getgroups() ([]int, error)** - получение перечня идентификаторов групп для приложения.
* **func Getpagesize() int** - получение размера страницы памяти в системе.
* **func Getpid() int** - получение идентификатора текущего процесса.
* **func Getppid() int** - получение идентификатора родительского процесса.
* **func Getuid() int** - получение идентификатора пользователя для приложения.
* **func Getwd() (dir string, err error)** - получение текущей папки.
* **func Hostname() (name string, err error)** - получение имени хоста.
* **func IsPathSeparator(c uint8) bool** - проверка, является ли указанный символ разделителем пути.
* **func Link(oldname, newname string) error** - создание хардлинка.
* **func LookupEnv(key string) (string, bool)** - проверка, есть ли указанная переменная окружения, её значение.
* **func Mkdir(name string, perm FileMode) error** - создание папки.
* **func MkdirAll(path string, perm FileMode) error** - создание папки со всеми родительскими папками, если необходимо. Если указанная папка уже существует, функция ничего не делает и возвращает nil.
* **func Pipe() (r \*File, w \*File, err error)** - создание пайпа.
* **func Readlink(name string) (string, error)** - чтение символической ссылки.
* **func Remove(name string) error** - удаление указанного файла.
* **func RemoveAll(path string) error** - удаление файлов по маске.
* **func Rename(oldpath, newpath string) error** - переименование файла.
* **func SameFile(fi1, fi2 FileInfo) bool** - проверка, не относятся ли два экземпляра FileInfo к одному и тому же файлу.
* **func Setenv(key, value string) error** - установка переменной окружения.
* **func Symlink(oldname, newname string) error** - создание символической связи.
* **func TempDir() string** - получение папки для временных файлов.
* **func Truncate(name string, size int64) error** - усечение файла до указанного размера.
* **func Unsetenv(key string) error** - удаление переменной окружения.
* **func UserCacheDir() (string, error)** - пользовательская папка для кэша. Как правило, `$HOME/.cache`.
* **func UserHomeDir() (string, error)** - домашнаяя папка пользователя, `$HOME`.

#### Процессы

```go
type Process struct {
        Pid int
        // contains filtered or unexported fields
}

type ProcAttr struct {
        // If Dir is non-empty, the child changes into the directory before
        // creating the process.
        Dir string
 
        // If Env is non-nil, it gives the environment variables for the
        // new process in the form returned by Environ.
        // If it is nil, the result of Environ will be used.
        Env []string
 
        // Files specifies the open files inherited by the new process. The
        // first three entries correspond to standard input, standard output, and
        // standard error. An implementation may support additional entries,
        // depending on the underlying operating system. A nil entry corresponds
        // to that file being closed when the process starts.
        Files []*File

        // Operating system-specific process creation attributes.
        // Note that setting this field means that your program
        // may not execute properly or even compile on some
        // operating systems.
        Sys *syscall.SysProcAttr
}
```

* **func FindProcess(pid int) (\*Process, error)** - поиск процесса по его идентификатору.
* **func StartProcess(name string, argv []string, attr \*ProcAttr) (\*Process, error)** - запуск процесса.
* **func (p \*Process) Kill() error** - принудительное завершение.
* **func (p \*Process) Release() error** - освобождение ресурсов, связанных со структурой `Process`.
* **func (p \*Process) Signal(sig Signal) error** - отправка сигнала процессу.
* **func (p \*Process) Wait() (\*ProcessState, error)** - ожидание завершения процесса.

Состояние процесса:

```go
type ProcessState struct {
        // contains filtered or unexported fields
}
```

* **func (p \*ProcessState) ExitCode() int** - код завершения.
* **func (p \*ProcessState) Exited() bool** - процесс завершился?
* **func (p \*ProcessState) Pid() int** - идентификатор процесса.
* **func (p \*ProcessState) String() string** 
* **func (p \*ProcessState) Success() bool** - процесс завершён успешно?
* **func (p \*ProcessState) Sys() interface{}** - зависящая от системы информация о процессе.
* **func (p \*ProcessState) SysUsage() interface{}** - зависящая от системы информация об использовании ресурсов.
* **func (p \*ProcessState) SystemTime() time.Duration** - время, проведённое процессом и его потомками в контексте ядра системы.
* **func (p \*ProcessState) UserTime() time.Duration** - время, проведённое процессом и его потомками в контексте пользователя.

