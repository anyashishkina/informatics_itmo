## Лабораторная работа № 1
```
#!/bin/bash

name="$*"
echo "Welcome, $name"
```
`name="$*"` содержит все параметры, введенные в командной строке

Например, при запуске файла 
`bash script.bash Benedict Timothy Carlton Cumberbatch`

будет выведено 
`Welcome, Benedict Timothy Carlton Cumberbatch`

## Лабораторная работа № 2
`ip_address="$1"` считываем IPv4-адрес
```
IFS='.'
read -a -r mas <<< "$ip_address"
```
считываем в массив mas числа из ip_address, разделенные "."

```
for el in "${mas[@]}"; do
        new_el=$(echo "obase=2;$el" | bc)
        new_el=$(printf "%08d" $new_el)
        new_ip_address="$new_ip_address.$new_el"
```
проходим по всем элементам массива mas, сначала переводим каждое число в двоичную форму, затем фиксируем длину 8 символов и собираем новую строку, ставя перед каждым числом "."

`echo "${new_ip_address:1}"` убираем ненужную точку в начале и выводим IP-адрес в двоичном формате

Итак, решение задачи:
```
#!/bin/bash

ip_address="$1"

IFS='.'
read -r -a mas <<< "$ip_address"

new_ip_address=""
for el in "${mas[@]}"; do
        new_el=$(echo "obase=2;$el" | bc)
        new_el=$(printf "%08d" $new_el)
        new_ip_address="$new_ip_address.$new_el"
done

echo "${new_ip_address:1}"
```

## Лабораторная работа № 4
После запуска aafire в контейнере:

<img width="569" alt="fire" src="https://github.com/anyashishkina/informatics_itmo/assets/95246399/5cb01f8a-6e15-4465-b642-f408100ba735">

## Лабораторная работа 5

## Введение

1 Создаю репозитория на GitHub

2 Клонирование репозитория:
```console
(base) annashishkina@MacBook-Pro-Anna ITMO github % git clone https://github.com/anyashishkina/git-practice.git
(base) annashishkina@MacBook-Pro-Anna ITMO github % cd git-practice 
```
3 Добавление файла:
```console
(base) annashishkina@MacBook-Pro-Anna ITMO github % git clone https://github.com/anyashishkina/git-practice.git
(base) annashishkina@MacBook-Pro-Anna ITMO github % cd git-practice 
(base) annashishkina@MacBook-Pro-Anna git-practice % touch example.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % vim example.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % git add example.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "File added example.txt"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin main
```
4 Создание ветки:
```console
git branch feature-branch
git checkout feature-branch
```
5 Отредактируйте файл example.txt, добавив еще текст.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim example.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % git add example.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Added chapter 4 in example.txt"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin feature-branch     
```
6 Слияние изменений:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout main
(base) annashishkina@MacBook-Pro-Anna git-practice % git merge feature-branch
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin main
```
### Завершение: все сработало правильно

## Работа с ветками
1 Создайте новый текстовый файл с базовой структурой книги
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % touch book.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % vim book.txt 
```
2 Создайте ветку "feature-login" для разработки новой функциональности:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout -b feature-login
```
3 Внесите изменения в файл:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim book.txt
```
4 Завершите изменения, закоммитьте их и отправьте ветку на GitHub:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add README.md
(base) annashishkina@MacBook-Pro-Anna git-practice % git add book.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Добавлена глава 3: Вход в систему"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin feature-login
```
## Работа с удаленным репозиторием
1 Переключитесь на основную ветку (main) и внесите изменения:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout main
```
2 Внесите изменения в основной ветке (например, добавьте описание книги):
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim example2.txt       
```
3 Закоммитьте изменения и отправьте их на GitHub:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add example2.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Изменено название книги и введение"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin main
```
## Моделирование конфликта
1 Вернитесь в ветку "feature-login" и внесите изменения в том же участке:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout feature-login
```
2 Измените главу 2 в файле
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim example2.txt    
```
3 Закоммитьте изменения и отправьте их на GitHub:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add example2.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Добавлен раздел о магии конфликтов"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin feature-login
```
## Разрешение конфликта
1 Вернитесь в основную ветку и попробуйте слить изменения:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout main
(base) annashishkina@MacBook-Pro-Anna git-practice % git pull origin main
```
Возникновение конфликта:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git merge feature-login 
Автослияние example2.txt
КОНФЛИКТ (добавление/добавление): Конфликт слияния в example2.txt
Сбой автоматического слияния; исправьте конфликты, затем зафиксируйте результат.
```
2 Возникнет конфликт. Разрешите его в файле
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim example2.txt
```
3 Закоммитьте разрешение конфликта и отправьте изменения на GitHub:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add example2.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Resolved conflict in chapter 2"
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin main
```
## Автоматизация проверки формата файлов при коммите
1 Создайте bash-скрипт (например, check_format.sh), который будет выполнять проверку формата .txt файлов. 
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim check_format.sh
```
bash-скрипт проверяет, чтобы сроки в txt файлах начинались с большой буквы.
![Изображение](images/code.png)
Запишу "hello world" в файл test.txt и попробую его закоммитить
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % echo "hello world" > test.txt
```
В результате проверки коммит отменён.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add test.txt 
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "проверка на формат"  
Проверка файла: test.txt
Ошибка: Файл 'test.txt' содержит строки, которые не начинаются с заглавной буквы.
Форматирование файлов не прошло проверку. Коммит отменен.
```
Теперь запишу в тот же файл Hello world.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % echo "Hello World" > test.txt
```
Теперь прошёл.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add test.txt
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "изменённый commit" 
Проверка файла: test.txt
Все файлы прошли проверку формата.
[main 32dd970] изменённый commit
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```
## Использование Git Flow в проекте
1 Убедитесь, что Git Flow установлен на локальной машине:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % brew install git-flow
```
2 В корне репозитория выполните инициализацию Git Flow.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git flow init     

Which branch should be used for integration of the "next release"?
   - develop
   - feature-branch
   - feature-login
Branch name for "next release" development: [develop] develop

How to name your supporting branch prefixes?
Feature branches? [feature/] 
Release branches? [release/] 
Hotfix branches? [hotfix/] 
Support branches? [support/] 
Version tag prefix? [] (base) annashishkina@MacBook-Pro-Anna git-practice % echo "Hello World" > test.txt
```
3 Создайте ветку для новой функциональности "task-management":
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git flow feature start task-management
Переключились на новую ветку «feature/task-management»

Summary of actions:
- A new branch 'feature/task-management' was created, based on 'develop'
- You are now on branch 'feature/task-management'

Now, start committing on your feature. When done, use:

     git flow feature finish task-management

```
4 Внесите изменения в код для добавления функционала управления задачами (например, в файл task_manager.py):
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % vim task_manager.py
```
Выполните коммит изменения по мере разработки:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git add task_manager.py
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Добавлен функционал управления задачами"
```
5 После завершения разработки функции завершите фичу и объедините ее с основной веткой:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git flow feature finish task-management 

Переключились на ветку «develop»
Обновление 32dd970..375d22c
Fast-forward
 task_manager.py | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 task_manager.py
Ветка feature/task-management удалена (была 375d22c).

Summary of actions:
- The feature branch 'feature/task-management' was merged into 'develop'
- Feature branch 'feature/task-management' has been removed
- You are now on branch 'develop'

```
6 Переключитесь на ветку "develop" и начните создание релиза:
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git checkout develop                   
Уже на «develop»
```
7 Внесите изменения, связанные с релизом (например, обновите версию в файле version.txt):
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % echo "V1.0.0" > version.txt                      
(base) annashishkina@MacBook-Pro-Anna git-practice % git add version.txt                               
(base) annashishkina@MacBook-Pro-Anna git-practice % git commit -m "Обновлена версия для релиза v1.0.0"

Проверка файла: version.txt
Все файлы прошли проверку формата.
[release/v1.0.0 648b86e] Обновлена версия для релиза v1.0.0
 1 file changed, 1 insertion(+)
 create mode 100644 version.txt
```
8 Завершите релиз и объедините его с ветками "develop" и "main":
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git flow release finish v1.0.0
```
Никаких критических ошибок не возникло. Завершение работы и отправка изменений на удаленный репозиторий.
```console
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin develop
Перечисление объектов: 11, готово.
Подсчет объектов: 100% (11/11), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (8/8), готово.
Запись объектов: 100% (10/10), 1.14 КиБ | 1.14 МиБ/с, готово.
Всего 10 (изменений 3), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (3/3), done.
remote: 
remote: Create a pull request for 'develop' on GitHub by visiting:
remote:      https://github.com/anyashishkina/git-practice/pull/new/develop
remote: 
To https://github.com/anyashishkina/git-practice.git
 * [new branch]      develop -> develop
(base) annashishkina@MacBook-Pro-Anna git-practice % git push origin main
Перечисление объектов: 1, готово.
Подсчет объектов: 100% (1/1), готово.
Запись объектов: 100% (1/1), 231 байт | 231.00 КиБ/с, готово.
Всего 1 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
To https://github.com/anyashishkina/git-practice.git
   830290e..1f321fb  main -> main
```



