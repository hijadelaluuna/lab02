## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [X] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Выполнить инструкцию учебного материала
- [X] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Создание переменных окружения 'GITHUB_USERNAME,GITHUB_EMAIL, 'GITHUB_TOKEN , а также связывание команды edit с вызовом текстового редактора Sublime Text.

$ export GITHUB_USERNAME=hijadelaluuna
$ export GITHUB_EMAIL=anastasiyasechina46@gmail.com
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=nano

Начало работы в рабочем каталоге **workspace** и активация исполняемых файлов.

$ cd $hijadelaluuna/workspace
$ source scripts/activate

Создание директории **~/.config** и файлa 'hub.

$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: $hijadelaluuna
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https

Создание каталога для хранения локальной копии удаленного репозитория.


$ mkdir projects/lab02 && cd projects/lab02
$ git init # Инициализация репозитория.
$ git config --global user.name $hijadelaluuna
$ git config --global user.email $anastasiyasechina46@gmail.com
# check your git global settings
$ git config -e --global
[user]
        email = anastasiyasechina46@gmail.com
        name = hijadelaluuna
[hub]
        protocol = https
$ sudo git remote add origin https://github.com/$hijadelaluuna/lab02.git # Подключение локального репозитория к удаленному серверу
$ sudo git remote -v # Список удаленных репозиториев, настроенных в данный момент
origin	https://github.com/hijadelaluuna/lab02.git (fetch)
origin	https://github.com/hijadelaluuna/lab02.git (push)
$ sudo git pull origin master
$ sudo touch README.md # Установка времени последнего изменения файла
$ git status # Список измененных файлов
$ sudo git add README.md # Добавление файлов в индекс
$ sudo git commit -m"added README.md"
[master (корневой коммит) 47b92e9] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
$ git push origin master


Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

*build*/
*install*/
*.swp
.idea/


$ git pull origin master # Объединение изменений, присутствующих в удаленном репозитории, в локальный рабочий каталог
$ git log # Список коммитов за все время существования репозитория.
commit 47b92e954b7eec9ee446e90764b8d0b86daf7740 (HEAD -> master)
Author: hijadelaluuna <anastasiyasechina46@gmail.com>
Date:   Sun Apr 21 18:10:13 2019 +0000

    added README.md

Создание директорий в рабочем каталоге и заголовочного файла **print.cpp** в локальном репозитории.

$ sudo mkdir sources
$ sudo mkdir include
$ sudo mkdir examples
$ cat > sources/print.cpp <<EOF # Создание файла с расширением .hpp
#include <print.cpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF



$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF



$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF



$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF

$ edit README.md


```ShellSession
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report


$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
