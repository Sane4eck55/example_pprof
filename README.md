# example_pprof

### 1. встраиваем в наш код
```
import (
    "net/http"
    _ "net/http/pprof"
)

func main() {
    // Запускаем HTTP сервер для доступа к pprof
    go func() {
        log.Println(http.ListenAndServe("localhost:6060", nil))
    }()

    // остальной код вашего приложения
}
```
### 2. Собираем данные для анализа

### CPU профиль
Выполните запрос к /debug/pprof/profile?seconds=30 (например, через браузер или curl) или используйте команду:
go tool pprof http://localhost:6060/debug/pprof/profile?seconds=30

### Heap (память)
Для получения информации о выделенной памяти:
```bash

go tool pprof http://localhost:6060/debug/pprof/heap
```
### Goroutines (состояние горутин)

```bash

go tool pprof http://localhost:6060/debug/pprof/goroutine
```
### Block profile (блокировки)

```bash

go tool pprof http://localhost:6060/debug/pprof/block
```
### 3. Анализ профилей
После получения файла профиля (.pb.gz), откройте его командой:

```bash

go tool pprof <файл_профиля>
```
### Визуализация результатов 
для mac выполнить brew install graphviz, после установки dot -V проверить все ли устаноилось
```bash
(pprof) web
```

https://github.com/google/pprof/blob/main/doc/README.md#interpreting-the-callgraph
