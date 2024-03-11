## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
  - Создан репозиторий lab02 на сервисе github.com
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
  - Создан файл README.md и .gitignore
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```sh
#include <iostream>
using namespace std;
int main(){
    cout << "Hello world" << endl;
    return 0;
}   
```
4. Добавьте этот файл в локальную копию репозитория.
  ```
 $ git add hello_world.cpp
```
5. Закоммитьте изменения с *осмысленным* сообщением.
 ```
  $ git commit -m"hello_world.cpp add"
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
 ```
 $ nano hello_world.cpp
```
```sh
#include <iostream>
#include <string>
using namespace std;
int main(){
    string name;
    cin>>name;
    cout << "Hello world from" << name <<endl;
    return 0;
}
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
 ```
 $ git commit -m"hello_world.cpp with name"
```
 > git add обновляет запись в индексе для hello_world.cpp с указанием на новый блоб.

8. Запуште изменения в удалёный репозиторий.
 ```
 $ git push origin master
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
 ```
 $ git log
```
 - история комитов на гитхабе

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```
$ git branch patch1
$ git switch patch1
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
#include <iostream>
#include <string>
int main(){
    std::string name;
    std::cin>>name;
    std::cout << "Hello world from" << name <<std::endl;
    return 0;
}
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```
$ git add hello_world.cpp
$ git commit -m"hello_world no namespace"
$ git push origin patch1
```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
 - Сделано
5. Создайте pull-request `patch1 -> master`.
 - Сделано
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
```sh
#include <iostream> //подключаем библиотеки
#include <string>
int main(){
    std::string name; //объявление переменной
    std::cin>>name; //считывание
    std::cout << "Hello world from" << name <<std::endl; //вывод
    return 0;
}
```
7. **commit**, **push**.
```
$ git add hello_world.cpp
$ git commit -m"hello_world no namespace + comments"
$ git push origin patch1
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
 - Изменения есть
9. В удалённый репозитории выполните  слияние PR `patch1 -> main` и удалите ветку `patch1` в удаленном репозитории.
 - Сделано
10. Локально выполните **pull**.
```
$ git pull origin patch1
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```
$ git log
```
```
zarok@ubuntu:~/projects/tp_labs/tp_projects/lab02$ git log
commit 988f9312910efe9f1d7b1775ab65fa0894d4aac5 (HEAD -> patch1, origin/patch1)
Author: Zarrokk <buranvoronezh6@gmail.com>
Date:   Tue Mar 12 00:12:20 2024 +0300

    hello_world no namespace + comments
```
12. Удалите локальную ветку `patch1`.
```
$ git branch -d patch1
```
### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```
$ git branch patch2
$ git switch patch2
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```
$ clang-format -style=mozilla -dump-config > .clang-format
$ clang-format -i *.cpp
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```
$ git add hello_world.cpp
$ git commit -m"hello_world clang"
$ it push origin patch2
````
 - pull request
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```
#include <iostream> //подключаем библиотеки.
#include <string>
int main(){
    std::string name; //объявление переменной
    std::cin>>name; //считывание
    std::cout << "Hello world from" << name <<std::endl; //output
    return 0;
}
```
5. Убедитесь, что в pull-request появились *конфликтны*.
![image](https://github.com/Zarrokk/lab02/assets/66065793/910a54f2-7c5b-4a1a-a031-d9a7cd26a25d)

6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```
$ git pull --rebase origin main
```
```
From https://github.com/Zarrokk/lab02
 * branch            main       -> FETCH_HEAD
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply acb3b8e... hello_world.cpp with name no namespace
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply acb3b8e... hello_world.cpp with name no namespace

```
```
$ git rebase --continue
```
```
Successfully rebased and updated refs/heads/patch2.
```
7. Сделайте *force push* в ветку `patch2`
```
$ git push origin patch2 --force
```
```
Username for 'https://github.com': Zarrokk
Password for 'https://Zarrokk@github.com': 
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.12 KiB | 384.00 KiB/s, done.
Total 9 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (4/4), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/Zarrokk/lab02/pull/new/patch2
remote: 
To https://github.com/Zarrokk/lab02.git
 * [new branch]      patch2 -> patch2

```
8. Убедитель, что в pull-request пропали конфликтны.
 - конфликтов нет
10. Вмержите pull-request `patch2 -> master`.
 -  Сделано
## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
