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

#### HEAD - всему голова

В выводе команды `git log` у верхнего в списке коммита (по умолчанию, без `--reverse`) можно заметить надпись `(HEAD -> master)`.
Это указатель на коммит, содержащийся в служебном файле `HEAD` внутри директории `.git`:

```bash
$ pwd # посмотрели, где мы
/Users/user/dev/first-project

$ cd .git/
$ ls # посмотрели, какие есть файлы
COMMIT_EDITMSG  ORIG_HEAD  description  index  logs/     refs/
HEAD            config     hooks/       info/  objects/

$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка
```

Внутри `HEAD` — ссылка на служебный файл: `refs/heads/master` (или `refs/heads/main` в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

```bash
$ cat refs/heads/master # взяли ссылку из файла HEAD
# внутри хеш
e007f5035f113f9abca78fe2149c593959da5eb7

$ git log 
# сверяем с хешем последнего коммита
commit e007f5035f113f9abca78fe2149c593959da5eb7
Author: John Doe <johndoe@example.com>
Date:   Tue Mar 28 00:26:53 2023 +0300

    Добавить амбиций в список дел

... # другие коммиты
```

#### Статусы файлов в Git

- `untracked` (неотслеживаемый) - Новые файлы в Git-репозитории помечаются как `untracked`, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У `untracked`-файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.
- `staged` (подготовленный) - После выполнения команды `git add` файл попадает в **staging area** (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.
Staging area также называют **index** (англ. «каталог») или **cache** (англ. «кеш»), а состояние файла `staged` иногда называют `indexed` или `cached`.
- `tracked` (отслеживаемый) - Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в staging area командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.
- `modified` (изменённый) - Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

#### Сто шагов назад (restore/reset)

- На случай, если необходимо выполнить анстейджинг (unstage) какого либо файла в выводе команды `git status` есть подсказка `use "git restore --staged <file>..." to unstage`.

Например:
```bash
$ touch example.txt # создали ненужный файл
$ git add example.txt # добавили его в staged

$ git status # проверили статус
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   example.txt

$ git restore --staged example.txt
$ git status # проверили статус

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        example.txt

no changes added to commit (use "git add" and/or "git commit -a")
# файл example.txt из staged вернулся обратно в untracked
```
Вызов `git restore --staged example.txt` перевёл `example.txt` из `staged` обратно в `untracked`.

Чтобы сбросить все файлы в одной директории из `staged` обратно в `untracked`/`modified` можно использовать команду `git restore --staged .`.
Точка (` . `) здесь обозначает `текущую директорию (папку)`.

- Если нужно откатить уже закоммиченные изменения - используется команда `git reset --hard <commit hash>` где commit hash это хеш коммита (его уникальный идентификатор). Простым языком эта команда вернёт всё к состоянию `указанного коммита` и удалит все последующие `после него`.
```bash
$ git log --oneline # хеш можно найти в истории
7b972f5 (HEAD -> master) style: добавить комментарии, расставить отступы
b576d89 feat: добавить массив Expenses и цикл для добавления трат # вот сюда и вернёмся
4b58962 refactor: разделить analyzeExpenses() на countSum() и saveExpenses()

$ git reset --hard b576d89
# теперь мы на этом коммите
HEAD is now at b576d89 feat: добавить массив Expenses и цикл для добавления трат
```
Теперь коммит b576d89 стал последним: вся дальнейшая разработка будет вестись от него. Файл также вернулся к тому состоянию, в котором был в момент этого коммита. А коммит 7b972f5 Git просто удалил. Это можно проверить, снова запросив лог. Он покажет следующее.
```bash
$ git log --oneline
b576d89 (HEAD -> master) feat: добавить массив Expenses и цикл для добавления трат
4b58962 refactor: разделить analyzeExpenses() на countSum() и saveExpenses()
```

- Если нужно откатить изменения, которые ещё не попали ни в `staging`, ни в коммит - `git restore <file>`.
```bash
# случайно изменили файл example.txt
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
          modified:   example.txt

$ git restore example.txt
$ git status
On branch main
nothing to commit, working tree clean
```

Изменения в файле «откатятся» до последней версии, которая была сохранена через `git commit` или `git add`.

Главное помнить, что `restore` работает только с файлами, а `reset` может работать с коммитами (ну и много чего ещё может).