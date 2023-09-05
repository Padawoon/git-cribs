### Шпаргалка по Git

#### Инициализация (создание) репозитория

- `cd` - перемещаться по директориям (Change Directory)
- `mv` - переместить или переименовать файл или директорию
- `git init` - делает директорию (папку) репозиторием
- `rm -rf .git` - удалить папку .git если нужно "разгитить" директорию

#### Работа с локальными изменениями

- `git status` - показывает состояние рабочей директории и индекса
- `git add` - добавляет файлы в индекс для будущего коммита
- `git commit` - создает коммит с сохраненными изменениями из индекса
- `git log` - выводит список всех коммитов в репозитории

#### Ветвление и слияние

- `git branch` - показывает список веток, текущая ветка помечена звездочкой
- `git checkout` - переключается между ветками
- `git merge` - объединяет изменения из одной ветки в другую

#### Работа с удаленными репозиториями (GitHub)

- `git remote` - показывает список удаленных репозиториев
- `git clone` - клонирует удаленный репозиторий на локальную машину
- `git push` - отправляет локальные изменения на удаленный сервер
- `git pull` - получает изменения с удаленного сервера и объединяет их с локальными изменениями
- `git fetch` - получает изменения с удаленного сервера, но не объединяет их

#### Работа с коммитами

- `git commit -m "сообщение коммита"` - создает коммит с сообщением о проделанных изменениях
- `git commit -a` - автоматически добавляет и коммитит все измененные файлы
- `git commit --amend` - изменяет последний коммит, добавляя новые изменения или исправляя сообщение

#### Инспекция и сравнение

- `git show` - показывает информацию о коммите и его изменениях
- `git log --graph` - выводит историю коммитов в виде графа
- `git blame` - показывает, кто и когда внес изменения в конкретные строки файла
- `git diff <commit> <commit>` - показывает разницу между двумя коммитами

#### Работа с ветками

- `git merge --no-ff` - объединяет ветки с созданием нового коммита с информацией о слиянии
- `git rebase` - перемещает коммиты из одной ветки на другую, создавая плоскую историю

#### Отмена изменений

- `git revert <commit>` - создает новый коммит, который отменяет изменения, внесенные в указанный коммит
- `git reset --hard <commit>` - отменяет изменения и перемещает указатель ветки на указанный коммит (осторожно, может стереть историю)
- `git checkout -- <file>` - отменяет изменения в указанном файле до последнего коммита

#### Работа с подмодулями

- `git submodule add <URL>` - добавляет подмодуль к проекту
- `git submodule update --init` - инициализирует и обновляет подмодули
- `git submodule foreach` - выполняет команду внутри каждого подмодуля

#### Алиасы

Можно создавать собственные алиасы для команд, чтобы сократить длинные команды. Например:

```git config --global alias.co checkout```

После этого можно использовать ```git co``` вместо ```git checkout```.

#### Разное

- `gitignore` - файл, в котором перечисляются файлы и директории, которые Git должен игнорировать при отслеживании
- `git diff` - показывает разницу между состояниями файлов
- `git reset` - сбрасывает индексацию файлов (может быть использован с разными опциями для отмены коммитов)
- `git stash` - временно сохраняет изменения, чтобы переключиться на другую ветку без коммита

#### Хэш - идентификатор коммита

Хэширование - это способ преобразовать набор данных в так называемый слепок/фингерпринт.
Каждый хэш коммита уникален и создаётся автоматически с помощью алгоритма SHA-1 (Secure Hash Algorithm).
Обычно хэш содерджит в себе до 40 символов из цифр 0-9 и латинских букв от A до F в любом регистре.
Если знать хэш, то можно без труда найти и узнать всю информацию об искомом коммите в выводе команды `git log` о которой ниже.

#### Логи - наше всё

Команда `git log` выводит список коммитов, который содержит в себе хэш коммита (его уникальный идентификатор), автора, дату коммита с указанием часового пояса и сообщение в коммите.

По умолнчанию эта команда выводит список комиитов в обратном порядке - от последнего к первому.

Команда `git log --oneline` выведет краткий список коммитов в виде нескольких символов из хэша коммита и сообщения к этому коммиту.
Количество символов хэша выводимого этой коммандой определяется командой автоматически так, чтобы они были уникальны в пределах одного репозитория, но чаще всего от 6 символов.

Команда `git log --reverse` выведет список коммитов от первого к последнему. Опция `--reverse` может сочетаться с `--oneline`.