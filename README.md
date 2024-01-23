# Практичесская работа №1.

## Информация о GIT.

Git - это система управления версиями  распределенной архитектурой.
Проще говоря, это консольная утилита для отслеживания и ведения истории изменения файлов в вашем проекте.
С помощью Git вы можете откатить свой проект до более старой версии, сравнивать, анализировать и сливать свои изменения в репозиторий.

Репозиторием называют хранилище вашего кода и историю его изменений. Git работает локально, и все ваши репозитории хранятся в определенных папках на жестком диске.

## Установка Git и натсройка. (Ubuntu, Debian).

Для утановки открываем терминал и вводим следующую команду:

```
sudo apt install git 
git version
```

Указать имя пользователя и эл. почты:

```
git config --global user.name "ваше_имя"
git config --global user.email "<адрес_почты@email.com>"
```
Чтобы убедиться, что изменения внесены, введите команду:

```
cat ~/.gitconfig 
```

## Создание репозитория.

```
cd <путь_к_вашему_проекту>
git init
```

"_Разгитить_" папку можно с помощью команды:

```
rm -rf .git # удалили подпапку .git
```

Теперь выбранная директория является репозиторием.
Проверить состояние репозитория:

```
git status
```
Команда git status выведет:

название текущей ветки: On branch master или On branch main;
сообщение о том, что в репозитории ещё нет коммитов: No commits yet;
сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — nothing to commit (create/copy files and use "git add" to track).

В отличие от git init, команду git status используют часто. В любой непонятной ситуации стоит посмотреть состояние (статус) репозитория, а потом решить, что делать дальше.

## Добавляем файлы в репозиторий.

Подготовить файлы к сохранению:

```
git add "название_файла" # можно использовать команду git --all, чтобы добавить сразу все файлы в репозиторий.
```

Теперь посмотрев статус репозитория, вы увидите, что были внсены изменения.

## Коммит.

Коммит — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться».
Это как если бы вы могли выполнить операцию Ctrl+Z для целой папки (репозитория).
Сделать коммит можно командой git commit c ключом -m (от англ. message — «сообщение»), который присваивает коммиту сообщение.

Просмотреть историю коммитов — 

```
git log
```

### Создание проекта на GitHub.

GitHub — платформа для хранения IT-проектов и совместной работы над ними с использованием Git. По сути, это сайт, куда можно загрузить файлы своего проекта для обмена с другими людьми.

Перед началом предлагаю зарегистрироваться на GitHub.

## Создаем удаленный репозиторий.

1. Создайте репозиторий. Для этого перейдите на вкладку Repositories (англ. «репозитории»), а затем нажмите на зелёную кнопку New (англ. «новый») справа. 
2. Открылось окно создания нового репозитория. Назовите его first-project.
   Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, будем называть их одинаково. 
   Другие поля вам пока не понадобятся. Смело нажимайте на зелёную кнопку Create repository (англ. «создать репозиторий») внизу.

## SSH-keys.

Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети.
Проверить наличие:

```
$ ls -la .ssh/ # вывели список созданных ключей 
```

Если папка пустая или её нет, всё в порядке. 
Если есть файлы с похожими названиями, SSH-ключи уже создавались:

```
    id_dsa.pub;
    id_ecdsa.pub;
    id_ed25519.pub;
    id_rsa.pub.
```

### Генерация SSH-ключа.

Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.

```
ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```


Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.

После ввода отобразится такое сообщение.

> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 

Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.

```
ls -a ~/.ssh
```
На экране должны появиться два файла — один с расширением .pub, другой — без.

### Инструкция по связыванию SSH-ключа и GitHub-аккаунта.

1. Скопируйте содержимое файла с публичным ключом в буфер обмена.
2. Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.
3. В меню слева нажмите на пункт SSH and GPG keys.
4. В открывшейся вкладке выберите New SSH key.
5. В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).
6. В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).
7. В поле Key скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку Add SSH key.
9. Проверьте правильность ключа с помощью следующей команды:

```
ssh -T git@github.com 
```

### Связываем локальный и удаленный репозитории.

Привязать удалённый репозиторий к локальному — git remote add

```
cd ~/dev/first-project
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git 
```

Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.

Убедиться, что репозитории связаны, — git remote -v

```
git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```


Отправить изменения на удалённый репозиторий — git push.
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin


```
 git push -u origin main
```

Если команда приведёт к ошибке, попробуйте  заменить main на master. 

Далее проверяем в репозиториии на GitHub наличие новых файлов с изменениямию
В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push.

# Хеширование. Лог. HEAD. Статусы. Чтение git status.

## Хеш.

Хеширование (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их «отпечаток» (англ. fingerprint).
Git хеширует (преобразует) информацию о коммите с помощью алгоритма SHA-1
(от англ. Secure Hash Algorithm — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш — результат хеширования.
- если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
- если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

Хеш — основной идентификатор коммита
Git хранит таблицу соответствий хеш → информация о коммите. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов.
Можно сказать, что хеш — основной идентификатор коммита.
При работе с Git хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным Git-командам, чтобы указать, с каким коммитом нужно произвести то или иное действие.
Все хеши и таблицу хеш → информация о коммите Git сохраняет в служебные файлы. Они находятся в скрытой папке .git в репозитории проекта.

## Лог.

После вызова git log появляется список коммитов.
Описание состоит из:
- Author — имя автора и его электронная почта;
- Date — дата и время создания коммита;
- в конце находится сообщение коммита.

Получить сокращённый лог — git log --oneline
Получить сокращённый лог можно с помощью команды git log с флагом --oneline (англ. «одной строкой»). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.

## HEAD.

Файл HEAD (англ. «голова», «головной») — один из служебных файлов папки .git. Он указывает на коммит, который сделан последним (то есть на самый новый).
В этом можно убедиться с помощью терминала. Перейдите в папку .git командой cd. Посмотрите содержимое файла HEAD командой cat.

Внутри HEAD — ссылка на служебный файл: refs/heads/master (или refs/heads/main в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

Когда вы делаете коммит, Git обновляет refs/heads/master — записывает в него хеш последнего коммита. Получается, что HEAD тоже обновляется, так как ссылается на refs/heads/master.

## Статусы файлов.

### Статусы untracked/tracked, staged и modified.

- untracked (англ. «неотслеживаемый»)

Мы говорили, что новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. 
У untracked-файла нет предыдущих версий, зафиксированных в коммитах или через команду git add.

- staged (англ. «подготовленный»)

После выполнения команды git add файл попадает в staging area (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит.
В этот момент файл находится в состоянии staged.
В одном из предыдущих уроков мы сравнили коммит с фотографией. Можно развить эту аналогию и сказать, что команда git add добавляет персонажей (текущее содержимое файла или нескольких файлов)
на сцену (англ. stage) для общей фотографии, а git commit делает снимок всей сцены целиком. 

- tracked (англ. «отслеживаемый»)

Cостояние tracked — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы,
которые были добавлены в staging area командой git add. То есть все файлы, в которых Git так или иначе отслеживает изменения.

- modified (англ. «изменённый»)

Состояние modified означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

### Про staged и modified

Команда git add добавляет в staging area только текущее содержимое файла. Если вы, например, сделаете git add file.txt, а затем измените file.txt, то новое содержимое файла не будет находиться в staging.
Git сообщит об этом с помощью статуса modified: файл изменён относительно той версии, которая уже в staging. Чтобы добавить в staging последнюю версию, нужно выполнить git add file.txt ещё раз.

## Цикл жизни файла GIT.

1. Файл только что создали. Git ещё не отслеживает содержимое этого файла. Состояние: untracked.
2. Файл добавили в staging area с помощью git add. Состояние: staged (+ tracked).

- Возможно, изменили файл ещё раз. Состояния: staged, modified (+ tracked).
- Обратите внимание: staged и modified у одного файла, но у разных его версий.
- Ещё раз выполнили git add. Состояние: staged (+ tracked).

3. Сделали коммит с помощью git commit. Состояние: tracked.
4. Изменили файл. Состояние: modified (+ tracked).
5. Снова добавили в staging area с помощью git add. Состояния: staged (+ tracked).
6. Сделали коммит. Состояния: tracked.
7. Повторили пункты 4−7 много-много раз.

### Как читать git status.

Какие состояния показывает git status
Большинство файлов в типичном проекте будут находиться в состоянии tracked (то есть закоммичены и не изменены после коммита). Вы не увидите это состояние в выводе команды git status — иначе она бы каждый раз выводила список вообще всех файлов проекта.
В итоге git status показывает только следующие состояния файлов:

- staged (Changes to be committed в выводе git status);
- modified (Changes not staged for commit);
- untracked (Untracked files).

## Типичные варианты вывода git status

Рассмотрим четыре примера состояний, в которых может находиться ваш репозиторий.

1. Нет ни staged-, ни modified-, ни untracked-файлов.

Если ничего не менять в git-status-lesson после первого коммита, то в нём не должно быть ни изменённых файлов (modified), ни новых (untracked), ни добавленных в список на коммит (staged).
Вызовите команду git status. Её вывод будет примерно таким.

```
git status
On branch master
nothing to commit, working tree clean  
```

Это означает, что в репозитории нет новых или изменённых файлов. Последняя строка nothing to commit, working tree clean буквально переводится как «нечего коммитить, рабочая директория чиста».
Первая строка On branch master сообщает, что текущая ветка — master.

2. Найдены неотслеживаемые файлы.

Создайте в папке ~/home/'user_name'/second-project файл fileA.txt. Теперь в репозитории есть новый файл в состоянии untracked. Снова вызовите команду git status. Результат будет таким.

```
touch fileA.txt
git status
On branch master
Untracked files: # найдены неотслеживаемые файлы
(use "git add <file>..." to include in what will be committed)
fileA.txt

nothing added to commit but untracked files present (use "git add" to track) 
```

Файл fileA.txt отображается в секции неотслеживаемых файлов — Untracked files. Это значит, что он не был добавлен в репозиторий через git add. 
Добавьте fileA.txt в staging area с помощью git add и снова запросите git status.

```
git add fileA.txt 
git status
On branch master
Changes to be committed: # новая секция
  (use "git restore --staged <file>..." to unstage)
        new file:   fileA.txt 
```

Теперь fileA.txt находится в секции Changes to be committed (англ. «изменения, которые попадут в коммит»).
Если сейчас выполнить коммит, то в репозитории будет зафиксирована текущая версия этого файла. Закоммитьте его.

```
git commit -m 'Добавить файл fileA.txt'
# тут будет вывод комманды commit, он нас не интересует
git status
On branch master
nothing to commit, working tree clean 
```

Вывод команды git status такой же, какой был после первого коммита: «Директория чиста».

3. Найдены изменения, которые не войдут в коммит

Теперь откройте файл fileA.txt и добавьте в него несколько слов — например, Это файл A!. Сохраните fileA.txt и вызовите команду git status. Её результат будет такой.

```
# внесли в fileA.txt правки
# запросили статус
git status 
On branch master
Changes not staged for commit: # ещё одна секция
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   fileA.txt 
```

Файл fileA.txt был изменён, но ещё не добавлен в staging area после этого. Так он оказался в секции Changes not staged for commit (англ. «изменения, которые не подготовлены к коммиту»). Эта секция соответствует статусу modified.
Подготовьте правки к коммиту с помощью git add.

```
git add fileA.txt
$ git status
On branch master
Changes to be committed: # все изменения готовы к коммиту
  (use "git restore --staged <file>..." to unstage)
        modified:   fileA.txt 
```

Теперь в коммит попадёт уже новая версия файла fileA.txt.

4. Файл добавлен в staging area, но после этого изменён

Вы добавили файл в staging area, но перед самым коммитом вспомнили важную мелочь. Например, вместо одного восклицательного знака в конце строки Это файл A! нужно поставить три.
Откройте текстовый редактор и добавьте нужные правки. Теперь можно выполнить коммит, но в любой непонятной ситуации сначала стоит вызвать git status. Он покажет следующее.

```
# изменили fileA.txt
git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
          modified:   fileA.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
          modified:   fileA.txt 
```

Файл попал и в staged (Changes to be committed), и в modified (Changes not staged for commit). В staging area находится версия файла с одним восклицательным знаком, а в Changes not staged for commit — уже изменённая версия, с тремя.
Чтобы закоммитить самую свежую версию файла, нужно снова выполнить git add перед коммитом.
Теперь проверьте, как вы усвоили материал урока! Изучите скриншот с выводами команды git status для репозитория quiz-project.

## Оформление коммитов. 

# Как откатывать назад.

Команда git restore --staged <file> переведёт файл из staged обратно в modified или untracked.
Команда git reset --hard <commit hash> «откатит» историю до коммита с хешем <hash>. Более поздние коммиты потеряются!
Команда git restore <file> «откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии.

# Изменения в файлах.

Команда git diff сравнит последнюю закоммиченную версию файла с той, что находится в состоянии modified.
Команда git diff --staged покажет изменения в staged-файлах относительно последних закоммиченных версий.

На этом всё про git diff! Эта команда поможет узнать, какие строки и в каких файлах изменились. Может быть полезно при поиске ошибок или чтобы разобраться, откуда появилась та или иная строка.
В этом уроке вы также познакомились с командой git diff <коммит1> <коммит2>. С её помощью удобно сравнивать изменения в двух коммитах.

# Игнорирование файлов в Git.

Замечательно! Игнорирование файлов — механизм, который нельзя игнорировать. Вот что важно помнить:

Если нужно, чтобы Git игнорировал какие-то файлы, стоит составить файл .gitignore.
Посмотреть, что игнорируется, можно с помощью команды git status --ignored.
Сам файл .gitignore — это обычный файл в репозитории. Его тоже стоит закоммитить.
Шаблонов много, но их легко найти в интернете вместе с примерами использования.
## Задача

Многие научные статьи оформляют с помощью TeX. Этот инструмент принимает на вход файлы с расширением .tex и выдаёт в качестве результата красиво оформленный .pdf.
Но есть подвох: в процессе работы TeX также создаёт много временных файлов с расширениями вроде .aux, .lof, .lot и так далее.
Составьте файл .gitignore так, чтобы Git игнорировал все файлы, кроме .tex и .pdf. Вы можете свериться с авторским решением, но сначала рекомендуем попробовать выполнить задание самостоятельно.

** # игнорирование всех файлов

!**.pdf # Исключения
!**.tex

# Работа с ветками в Git.

Команда git clone копирует проект на локальный компьютер.
git clone автоматически связывает локальный репозиторий с удалённым.

### Fork.












Данный раздел для самотстоятельного ГУГЛЕНИЯ.