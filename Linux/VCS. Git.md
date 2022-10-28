`diff -u file1 file2` -- позволяет вывести строки, отличающиеся между файлами в унифицированном формате

`patch old_file patch_file` -- перезаписывает старый файл с учетом изменений, лежащих во втором аргументе

---
## Первоначальная конфигурация

| Команда                        | Описание                                           |
| ------------------------------ | -------------------------------------------------- |
| `git config --local user.name` | Установить для текущего репозитория параметр имени |
| `git config --local user.name` | Установить для текущего репозитория параметр почты |
| `git config --global core.editor "nvim"` | Использовать `nvim` как редактор по умолчанию                                |                                                    |

## Инициализация репозитория

| Команда         | Описание                          |
| --------------- | --------------------------------- |
| `git clone url` | Клонирование репозитория по `url` |
| `git init`      | Создание пустого гит репозитория в текущей директории                                  |

## Отслеживание

*Staging area (index)* -- файл, поддерживаемый Git'ом, который содержит всю информацию о том, какие файлы и изменения войдут в следующий комит

![[Images/VCS/staging_area.png]]

_Changes to be committed_ -- изменение в настоящий момент находится в *промежуточной области* (staging area)

| Команда        | Описание                                                                                |
| -------------- | --------------------------------------------------------------------------------------- |
| `git add file` | Доабвить `file` к списку отслеживаемых с помощью git  (переместить в staging area)                                  |
| `git status`   | Позволяет получить некоторую информацию о текущем рабочем дереве и ожидающих изменениях |
| `git commit`   |   Позволяет сохранить изменения из staging area в .git репозиторий                                                                                      |