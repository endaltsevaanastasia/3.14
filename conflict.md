[< На главную страницу](readme.md)

## **Конфликты GIT**

Системы контроля версий предназначены для управления дополнениями, вносимыми в проект множеством распределенных авторов (обычно разработчиков). Иногда один и тот же контент могут редактировать сразу несколько разработчиков. Если разработчик A попытается изменить код, который редактирует разработчик B, может произойти конфликт. Для предотвращения конфликтов разработчики работают в отдельных изолированных ветках. Основная задача команды git merge заключается в слиянии отдельных веток и разрешении любых конфликтующих правок.

### **Общие сведения:**

Слияние и конфликты являются неотъемлемой частью работы с Git. Git позволяет выполнять слияния очень просто. В большинстве случаев Git самостоятельно решает, как автоматически интегрировать новые изменения.

Обычно конфликты возникают, когда два человека изменяют одни и те же строки в файле или один разработчик удаляет файл, который в это время изменяет другой разработчик. В таких случаях Git не может автоматически определить, какое изменение является правильным. Конфликты затрагивают только того разработчика, который выполняет слияние, остальная часть команды о конфликте не знает. Git помечает файл как конфликтующий и останавливает процесс слияния.

### **Типы конфликтов:**

Конфликт во время слияния может произойти в двух отдельных точках — при запуске и во время процесса слияния. Далее рассмотрим, как разрешать каждый из этих конфликтных сценариев.

***Git прерывает работу в самом начале слияния:***

Выполнение команды слияния прерывается в самом начале, если Git обнаруживает изменения в рабочем каталоге или разделе проиндексированных файлов текущего проекта. Git не может выполнить слияние, поскольку иначе эти ожидающие изменения будут перезаписаны новыми коммитами. Такое случается из-за конфликтов не с другими разработчиками, а с ожидающими локальными изменениями. Локальное состояние необходимо стабилизировать с помощью команд `git stash`, `git checkout`, `git commit` или `git reset`.

***Git прерывает работу во время слияния:***

Сбой В ПРОЦЕССЕ слияния говорит о наличии конфликта между текущей локальной веткой и веткой, с которой выполняется слияние. Это свидетельствует о конфликте с кодом другого разработчика. Git сделает все возможное, чтобы объединить файлы, но оставит конфликтующие участки, чтобы вы разрешили их вручную.

### **Выявление конфликтов:**

При помощи комманды `git status` можно выявить конфликт. Он выводит файл с которым произошел конфликт. Для просмотра что именно случилось в файле используется комманда cat.

### **Разрешение конфликтов слияния при помощи команд GIT:**

Общие инструменты:
```
git status
```
Команда status часто используется во время работы с Git и помогает идентифицировать конфликтующие во время слияния файлы.
```
git log --merge
```
При передаче аргумента `--merge` для команды `git log` будет создан журнал со списком конфликтов коммитов между ветками, для которых выполняется слияние.
```
git diff
```
Команда `diff` помогает найти различия между состояниями репозитория/файлов. Она полезна для выявления и предупреждения конфликтов слияния.

### **Инструменты для случаев, когда Git прерывает работу в самом начале слияния:**
```
git checkout
```
Команда `checkout` может использоваться для отмены изменений в файлах или для изменения веток.
```
git reset --mixed
```
Команда `reset` может использоваться для отмены изменений в рабочем каталоге или в разделе проиндексированных файлов.

### **Инструменты для случаев, когда конфликты Git возникают во время слияния:**
```
git merge --abort
```
При выполнении команды `git merge` с опцией `--abort` процесс слияния будет прерван, а ветка вернется к состоянию, в котором она находилась до начала слияния.
```
git reset
```
Команду `git reset` можно использовать для разрешения конфликтов, возникающих во время выполнения слияния, чтобы восстановить заведомо удовлетворительное состояние конфликтующих файлов.