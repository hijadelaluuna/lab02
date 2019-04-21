
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
Начало работы в рабочем каталоге 'workspace и активация исполняемых файлов.

$ export GITHUB_USERNAME=hijadelaluuna
$ export GITHUB_EMAIL=anastasiyasechina46@gmail.com
$ export GITHUB_TOKEN= ca176118fade0e937d053401373c810b53f466f8
$ alias edit=nano


Создание директории **~/.config** и файлa 'hub.


$ cd $hijadelaluuna/workspace # Переход в  рабочую директорию.
$ source scripts/activate # Выполнение команд из файла 


Создание каталога для хранения локальной копии удаленного репозитория.

$ mkdir ~/.config # Создание директории ~/.config

$ cat > ~/.config/hub <<EOF
github.com:
- user: $hijadelaluuna
  oauth_token: $ca176118fade0e937d053401373c810b53f466f8
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
# Подключение локального репозитория к удаленному серверу
$ git remote add origin https://github.com/$hijadelaluuna/lab02.git 
$ git remote -v # Список удаленных репозиториев, настроенных в данный момент
origin	https://github.com/hijadelaluuna/lab02.git (fetch)
origin	https://github.com/hijadelaluuna/lab02.git (push)
$ git pull origin master # Объединение изменений, присутствующих в удаленном репозитории, в локальный рабочий каталог
From https://github.com/hijadelaluuna/lab02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
Already up to date.
$ touch README.md # Установка времени последнего изменения файла
$ git status # Список измененных файлов
On branch master
nothing to commit, working tree clean
$ git add README.md # Добавление файлов в индекс
$ git commit -m"added README.md" # Коммит изменений в файлах проекта
On branch master
nothing to commit, working tree clean
$ git push origin master # Помещение изменений в главную ветку удаленного хранилища, связанного с рабочим каталогом
Everything up-to-date

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:


*build*/
*install*/
*.swp
.idea/


Работа с репозиторием (пулл изменений из удаленного репозитория и просмотр истории коммитов).

$ git pull origin master # Объединение изменений, присутствующих в удаленном репозитории, в локальный рабочий каталог
$ git log # Список коммитов за все время существования репозитория.

Создание директорий в рабочем каталоге и заголовочного файла **print.cpp** в локальном репозитории.


$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF # Создание файла с расширением .hpp
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF

Создание и запись в заголовочный файл **print.hpp**

$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF

Создание и запись в исполняемый файл **example1.cpp**



$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF

Создание и запись в файл **example2.cpp**

$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF

Редактирование файла в локальной копии репозитория.

$ edit README.md



$ git status # Cписок измененных файлов
$ git add # Добавления текущего каталога в индекс.
$ git commit -m"added sources"
$ git push origin master


## Report


$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab$hijadelaluuna.git tasks/lab$lab02
$ mkdir reports/lab$lab02
$ cp tasks/lab$lab02/README.md reports/lab$lab02/REPORT.md
$ cd reports/lab$lab02
$ edit REPORT.md
$ gistup -m "lab02"
