| Команда | Описание                                      |
| ------- | --------------------------------------------- |
| `hjlk`  | ←  ↓  ↑  →                                    |
| `w`     | Перейти к символу перед следующим словом      |
| `e`     | Перейти к последнему символу текущего слова   |
| `$`     | Перейти к последнему символу текущей *строки* |
| `0`     | Перейти к первому символу текущей *строки*                                              |

| Команда    | Описание                         |
| ---------- | -------------------------------- |
| `123G`     | Перейти к строке `123`           |
| `Ctrl + O` | Вернуться в предыдущее место     |
| `Ctrl + i` | Вернуться в следующее место      |
| `%`        | Перейти к соответствующей скобке |

| Команда                       | Описание                                                          |
| ----------------------------- | ----------------------------------------------------------------- |
| `:/s/pattern/replacement`     | Заменить первое вхождение `pattern` на `replacement` в строке     |
| `:s/global_pat/global_repl/g` | Заменить все вхождения `global_pat` на `global_repl` в строке     |
| `:12,23s/old/new/g`           | Заменить `old` на `new` между 12 и 23 строками                    |
| `:%s/old/new/g`               | Заменить `old` на `new` во всем файле                             |
| `:%s/old/new/gc`              | Заменить `old` на `new` во всем файле с запросом на подтверждение |

| Команда     | Описание                           |
| ----------- | ---------------------------------- |
| `:!command` | Исполнить в bash команду `command` |

| Команда   | Описание                                                 |
| --------- | -------------------------------------------------------- |
| `:r TEST` | Вставить текст из файла `TEST` в текущее место курсора   |
| `:r !cmd` | Вставить результат команды `cmd` в текущее место курсора |

| Команда | Описание                          |
| ------- | --------------------------------- |
| `R`     | Режим непрерывной замены символов |

