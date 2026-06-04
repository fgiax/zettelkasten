# Гайд по файлу конфигурации Git `~/.gitconfig`

## Что такое `~/.gitconfig`

Файл `~/.gitconfig` содержит глобальные настройки Git для текущего пользователя.

Символ `~` обозначает домашний каталог пользователя.

Примеры расположения файла:

### Linux / Android (Termux)

```text
~/.gitconfig
```

Например:

```text
/data/data/com.termux/files/home/.gitconfig
```

Настройки из этого файла применяются ко всем репозиториям пользователя, если они не переопределены локально в `.git/config`.

---

## Уровни конфигурации Git

Git поддерживает три уровня настроек.

| Уровень    | Файл             | Команда               |
| ---------- | ---------------- | --------------------- |
| Системный  | `/etc/gitconfig` | `git config --system` |
| Глобальный | `~/.gitconfig`   | `git config --global` |
| Локальный  | `.git/config`    | `git config --local`  |

### Приоритет настроек

```text
Локальный > Глобальный > Системный
```

Если один и тот же параметр задан на нескольких уровнях, используется значение с более высоким приоритетом.

---

## Просмотр текущей конфигурации

Показать все настройки:

```bash
git config --list
```

Показать источник каждой настройки:

```bash
git config --list --show-origin
```

Показать конкретный параметр:

```bash
git config --global user.name
```

```bash
git config --global user.email
```

```bash
git config --global init.defaultBranch
```

Узнать, из какого файла получено значение:

```bash
git config --show-origin user.name
```

Пример:

```text
file:/data/data/com.termux/files/home/.gitconfig    John Doe
```

---

## Базовая настройка пользователя

Указать имя:

```bash
git config --global user.name "John Doe"
```

Указать email:

```bash
git config --global user.email "john@example.com"
```

В результате в `~/.gitconfig` появится:

```ini
[user]
    name = John Doe
    email = john@example.com
```

### Важно

Если файл `~/.gitconfig` ещё не существует, Git создаст его автоматически при выполнении первой команды вида:

```bash
git config --global ...
```

---

## Выбор ветки по умолчанию

Современные проекты обычно используют ветку `main`.

Установить её как ветку по умолчанию:

```bash
git config --global init.defaultBranch main
```

В файле `~/.gitconfig` появится:

```ini
[init]
    defaultBranch = main
```

Теперь новый репозиторий после команды:

```bash
git init
```

будет сразу создаваться с веткой:

```text
main
```

без предупреждения о выборе имени основной ветки.

### Что происходит автоматически

Команда:

```bash
git config --global init.defaultBranch main
```

создаёт (если необходимо) или изменяет файл:

```text
~/.gitconfig
```

и добавляет в него запись:

```ini
[init]
    defaultBranch = main
```

---

## Настройка редактора

Например, Neovim:

```bash
git config --global core.editor "nvim"
```

или Vim:

```bash
git config --global core.editor "vim"
```

Конфигурация:

```ini
[core]
    editor = nvim
```

Редактор используется для:

* сообщений коммитов;
* интерактивного rebase;
* редактирования конфигурации Git;
* создания и редактирования тегов.

---

## Цветной вывод

Включить цвета:

```bash
git config --global color.ui auto
```

Конфигурация:

```ini
[color]
    ui = auto
```

---

## Настройка переноса строк

Для Linux и Android обычно используется:

```bash
git config --global core.autocrlf input
```

Конфигурация:

```ini
[core]
    autocrlf = input
```

Это помогает избежать проблем с окончаниями строк между Linux и Windows.

---

## Полезные алиасы

Создать короткие команды:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
```

Конфигурация:

```ini
[alias]
    st = status
    co = checkout
    br = branch
    cm = commit
```

Использование:

```bash
git st
git co main
git br
git cm -m "Update"
```

---

## Красивый лог

Добавить алиас:

```bash
git config --global alias.lg \
"log --graph --oneline --decorate --all"
```

Конфигурация:

```ini
[alias]
    lg = log --graph --oneline --decorate --all
```

Использование:

```bash
git lg
```

Пример вывода:

```text
* 4f6c123 (HEAD -> main) Add login
* a2d7312 Update README
* b8f1045 Initial commit
```

---

## Современные команды Git

Начиная с Git 2.23 появились специальные команды.

Переключение между ветками:

```bash
git switch main
```

Создание новой ветки и переход на неё:

```bash
git switch -c feature
```

Восстановление файлов:

```bash
git restore file.txt
```

Ранее для этого часто использовалась универсальная команда:

```bash
git checkout
```

Поэтому алиас:

```bash
git config --global alias.co checkout
```

остаётся полезным для совместимости со старыми инструкциями и версиями Git.

---

## Удаление настроек

Удалить параметр:

```bash
git config --global --unset user.email
```

Удалить секцию целиком:

```bash
git config --global --remove-section alias
```

---

## Просмотр и редактирование файла

Открыть файл напрямую:

```bash
nvim ~/.gitconfig
```

или:

```bash
vim ~/.gitconfig
```

Открыть через Git:

```bash
git config --global --edit
```

---

## Формат файла

Файл `~/.gitconfig` использует формат INI.

Общий вид:

```ini
[section]
    key = value
```

Пример:

```ini
[user]
    name = John Doe
    email = john@example.com

[core]
    editor = nvim
```

Поэтому файл можно редактировать как вручную, так и через команды Git.

---

## Пример хорошего `~/.gitconfig`

```ini
[user]
    name = John Doe
    email = john@example.com

[init]
    defaultBranch = main

[core]
    editor = nvim
    autocrlf = input

[color]
    ui = auto

[alias]
    st = status
    co = checkout
    br = branch
    cm = commit
    lg = log --graph --oneline --decorate --all
```

---

## Где Git хранит эту информацию

Когда выполняется команда:

```bash
git config --global user.name "John Doe"
```

Git записывает значение в файл:

```text
~/.gitconfig
```

То есть команда:

```bash
git config --global ...
```

является удобным интерфейсом для чтения и изменения файла конфигурации без необходимости редактировать его вручную.

---

## Полезные ресурсы для изучения Git

### Официальная документация Git

[Git Documentation](https://git-scm.com/doc?utm_source=chatgpt.com)

Основной источник документации по Git. Содержит справку по всем командам и руководства. ([Git SCM][1])

### Официальный раздел Learn на сайте Git

[Git Learn](https://git-scm.com/learn?utm_source=chatgpt.com)

Бесплатные книги, видеоуроки, шпаргалки и дополнительные материалы для изучения Git. ([Git SCM][1])

### Книга Pro Git

[Pro Git Book](https://git-scm.com/book/en/v2?utm_source=chatgpt.com)

Одна из лучших бесплатных книг по Git от Scott Chacon и Ben Straub. Подходит как для новичков, так и для продвинутых пользователей. ([GitHub][2])

### GitHub Skills

[GitHub Skills](https://skills.github.com/?utm_source=chatgpt.com)

Интерактивные практические курсы по Git и GitHub прямо внутри GitHub. ([GitHub Docs][3])

### Git и GitHub Learning Resources

[GitHub Learning Resources](https://docs.github.com/get-started/quickstart/git-and-github-learning-resources?utm_source=chatgpt.com)

Подборка официальных материалов, курсов и упражнений по Git и GitHub. ([GitHub Docs][3])

### Полезная шпаргалка

[Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf?utm_source=chatgpt.com)

Краткий справочник по наиболее часто используемым командам Git.

---

## Рекомендуемый порядок изучения

1. Изучить базовые команды:

   * `git init`
   * `git status`
   * `git add`
   * `git commit`
   * `git log`

2. Освоить работу с удалёнными репозиториями:

   * `git clone`
   * `git remote`
   * `git push`
   * `git pull`

3. Изучить ветвление:

   * `git branch`
   * `git switch`
   * `git merge`

4. Разобраться с историей изменений:

   * `git diff`
   * `git restore`
   * `git reset`
   * `git revert`

5. Перейти к продвинутым темам:

   * `rebase`
   * `stash`
   * `tag`
   * `cherry-pick`
   * `bisect`
   * hooks
   * Git internals

---

## Краткий вывод

Файл `~/.gitconfig` — основной глобальный конфигурационный файл Git пользователя. В нём обычно настраиваются:

* имя и email автора;
* ветка по умолчанию (`main`);
* редактор;
* цветной вывод;
* правила обработки окончаний строк;
* пользовательские алиасы.

Знание структуры `~/.gitconfig` позволяет легко понимать, где Git хранит настройки и как управлять ими вручную при необходимости.

[1]: https://git-scm.com/learn?utm_source=chatgpt.com "Git - Learn"
[2]: https://github.com/progit?utm_source=chatgpt.com "Pro Git Book · GitHub"
[3]: https://docs.github.com/get-started/quickstart/git-and-github-learning-resources?utm_source=chatgpt.com "Git and GitHub learning resources - GitHub Docs"

