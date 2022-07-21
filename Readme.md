# Инструкция по работе с git и удалёнными репозиториями

## Что такое git?
*Git* одна из реализаций распредённых систем контроля версий. *Git* на данный момент является самой полулярной реализацией. Самой популярной реализацией *Git* является [GitHub](https://github.com) 

## Подготовка репозитория
Для того, чтобы создать репозиторий используется команда *git init*. Для этого необходимо написать в терминале в папке будущего репозитория *git init* 

## Состояние репозитория
Для того, чтобы посмотреть состояние репозитория, используется команда *git status* Для этого в терминале с папкой-репозиторием необходмо написать *git status*, и возможно увидеть несколько состояний:
1. Nothing to commit - репозиторий не содержит изменений
2. Unversioned file - папка содержит файл, к которому не добавлена версионность

# Просмотр сделанных изменений
Для того, чторбы просмотреть разницу между текущей версией файла, и версией файла в полследнем коммите, используется команда *git diff*. Для этого в терминале с папкой с репозиторием, напишите *git diff*

## Создание коммитов

### Добавление файла к коммиту

Для добавления файла к коммиту используется команда *git add*. Пишется она следующим образом *git add <имя файла>* в терминале в папке с созданным репозиторием.

### Создание нового коммита

Для создание нового "сохранения" испольузется команда *git commit*. Используется она следующим образом: в терминале с папкой-репозиторием пишется *git commit -m <сообщение к коммиту>*. Сообщение к коммиту писать **ОБЯЗАТЕЛЬНО**!!! 

## Отмена коммитов и перемещение по истории
Все коммиты, которые уже были отправлены в удалённый репозиторий, должны отменяться новыми коммитами (git revert), дабы избежать проблем с историей разработки у других участников проекта.

## создать новый коммит, отменяющий изменения последнего коммита без запуска редактора сообщения:
**git revert HEAD --no-edit**  
## то же, но отменяются изменения, внесённые коммитом с указанным хешем (b9533bb):
**git revert b9533bb --no-edit**

Все команды, приведённые ниже можно выполнять ТОЛЬКО если коммиты еще не были отправлены в удалённый репозиторий.
 

# ВНИМАНИЕ! Опасные команды, можно потерять незакоммиченные изменения
git commit --amend -m "Название"  
* «перекоммитить» изменения последнего коммита, заменить его новым коммитом с другим сообщением (сдвинуть текущую ветку на один коммит назад, сохранив рабочую директорию и индекс «как есть», создать новый коммит с данными из «отменяемого» коммита, но новым сообщением)

git reset --hard @~      
* передвинуть HEAD (и ветку) на предыдущий коммит, рабочую директорию и индекс сделать такими, какими они были в момент предыдущего коммита

git reset --hard 75e2d51
* передвинуть HEAD (и ветку) на коммит с указанным хешем, рабочую директорию и индекс сделать такими, какими они были в момент указанного коммита

git reset --soft @~ 
* передвинуть HEAD (и ветку) на предыдущий коммит, но в рабочей директории и индексе оставить все изменения

git reset --soft @~2     
* то же, но передвинуть HEAD (и ветку) на 2 коммита назад

git reset @~             
* передвинуть HEAD (и ветку) на предыдущий коммит, рабочую директорию оставить как есть, индекс сделать таким, каким он был в момент предыдущего коммита (удобнее, чем git reset --soft @~, если индекс нужно задать заново)

# Почти как git reset --hard, но безопаснее: не получится потерять изменения в рабочей директории
git reset --keep @~      # передвинуть HEAD (и ветку) на предыдущий коммит, сбросить индекс, но в рабочей дире

## Журнал изменений
Для просмотра журнала измений используется команда *git log*. Для этого в терминале в папке с репозиторием достаточно написать *git log*

## Перемещение между "сохранениями"
Для перемещения между сохранениями используется команда *git checkout*. Для того, чтобы перемиститься на указанный коммит в терминале в папке с репозиторием пишем *git checkout <номер коммита>*. **Номер коммита** берется из журнала изменений, о котором сказано выше. После перемещния на указанный коммит мы попадаем в состояние **detached head*. Чтобы вернуться к обычной работе, необходимо написать *git checkout master*.

## Ветки в git
Ветки в *git* нужны, чтобы работать с "чистовиком" и "черновиками". Для того, чтобы создать новую ветку используется команда *git branch*. В терминале в папке с репозиторием, напишите *git branch <название ветки>*.

## Слияние веток и разрешение конфликтов
Для слияния двух веток используется команда *git merge*. Для её использования необходимо перейти в ту веку, куда Вы хотите сделать слияние, после чего в терминале в папке с репозиторием написать *git merge <название сливаемой ветки>*. Чаще всего слияние проиходит автоматически, но возможны **КОНФЛИКТЫ**. В таком случае, необходимо вручную получить желаемую версию файла и сделать коммит.

## Удаление веток
Для удаления ветки используется команда *git branch -d*. Для этого необходимо в папке с репозиторием в терминале написать *git branch -d <название ветки>*. Удаляемая ветка **ОБЯЗАТЕЛЬНО** должна быть **СЛИТА**

## Получение удалённого репозитория
Для того, чтобы скачать удалённый репозиторий необходимо использовать команду *git clone*. В терминале, в котором открыта любая пустая папка, необходимо написать *git clone <ссылка на репозиторий>*. Репозиторий скачатеся в папку, название которой будет совпадать с названием репозитория.

## Скачивание изменений с удалённого репозитория
Для того, чтобы скачать изменения с удалённого репозитория, необходимо использовать команду *git pull*. В терминале с  папкой с репозиторием, связанным с удалённым репозиторием, пишем *git pull origin <название ветки>* для того, чтобы принять изменения из указанной ветки удалённго репозитория в текущую ветку.

## Отправка изменений Github
Для отправки изменений в удалённый репозиторий необходимо использовать команду *git push*. Для этого в терминале с папкой с репозиторием, связанным с удалённым репозиторием, пишем команду *git push origin <название ветки>*, <название ветки> - это ветка в удалённом репозитори, куда необходимо отправить совершённые изменения

## Удаление файла
git rm text.txt    
* удалить отслеживаемый неизменённый файл и проиндексировать это изменение

git rm -f text.txt 
* удалить отслеживаемый изменённый файл и проиндексировать это изменение

git rm -r log/     
* удалить всё содержимое отслеживаемой директории log/ и проиндексировать это изменение

git rm ind*        
* удалить все отслеживаемые файлы с именем, начинающимся на «ind» в текущей директории и проиндексировать это изменение

git rm --cached readme.txt 
* удалить из отслеживаемых индексированный файл (ФАЙЛ ОСТАНЕТСЯ НА МЕСТЕ) (часто используется для нечаянно добавленных в отслеживаемые файлов)

## Удалённые репозитории
Есть два распространённых способа привязать удалённый репозиторий к локальному: по HTTPS и по SSH. Если SSH у вас не настроен (или вы не знаете что это), привязывайте удалённый репозиторий по HTTPS (адрес привязываемого репозитория должен начинаться с https://).

git remote -v              
* показать список удалённых репозиториев, связанных с локальным

git branch -r              
* показать удаленные ветки

git branch -a              
* показать все ветки(локальные и удаленные)       

git remote remove origin   
* убрать привязку удалённого репозитория с сокр. именем origin

git remote add origin https://github.com:nicothin/test.git 
* добавить удалённый репозиторий (с сокр. именем origin) с указанным URL

git remote rm origin       
* удалить привязку удалённого репозитория

git remote show origin     
* получить данные об удалённом репозитории с сокращенным именем origin

git fetch origin           
* скачать все ветки с удаленного репозитория (с сокр. именем origin), но не сливать со своими ветками

git fetch origin master    
* то же, но скачивается только указанная ветка

git checkout --track origin/github_branch 
* создать локальную ветку 

github_branch (данные взять из удалённого репозитория с сокр. именем origin, ветка github_branch) и переключиться на неё
git push origin master     
* отправить в удалённый репозиторий (с сокр. именем origin) данные своей ветки master

git pull origin            
* влить изменения с удалённого репозитория (все ветки)

git pull origin master     
* влить изменения с удалённого репозитория (только указанная ветка)

## Теги
git tag v1.0.0               
* создать тег с указанным именем на коммите, на который указывает HEAD

git tag -a -m 'В продакшен!' v1.0.1 master 
* создать тег с описанием на том коммите, на который смотрит ветка master

git tag -d v1.0.0           
* удалить тег с указанным именем(ами)

![git](bear-cavalry.png)