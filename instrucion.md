# Работа с Git
## Основы Git
Git — (текст для слияния с конфликтом) это система контроля версий (VCS), которая позволяет отслеживать и фиксировать изменения в коде: вы можете восстановить код в случае сбоя или откатить до более ранних версий. А ещё это must-have инструмент для взаимодействия нескольких разработчиков на одном проекте.

С Git работают через командную строку или инструменты вроде GitHub Desktop. Команды Git принимают вид git <команда> <аргументы>, где аргументом может быть путь к файлу. В команды также включаются опции, которые обозначаются как --<опция>. Забыли, как использовать команду? Откройте руководство с git help <команда>.
## Основные команды
* **git init** - инициализация локального репозитория
* **git status** - получение информации о текущем состоянии git
* **git add**  - добавить файл или файлы к следующему коммиту
* **git commit -m "*message*"** - создание коммита с комментарием 
* **git log** - вывод на экран истории всех коммиитов с их хеш-кодами
* **git chekout** - переход от одного коммита к другому
* **git chekout master** - переход к актуальному состоянию
* **git diff** - oтобразить разницу между текущим сохранненым файлом и заккомиченным файло
## Файловая система
Команда git status отображает все файлы, которые различаются между тремя разделами. У файлов есть 4 состояния:

1. Неотслеживаемый (untracked) — находится в рабочей директории, но нет ни одной версии в HEAD или в области подготовленных файлов (Git не знает о файле).
2. Изменён (modified) — в рабочей директории есть более новая версия по сравнению с хранящейся в HEAD или в области подготовленных файлов (изменения не находятся в следующем коммите).
3. Подготовлен (staged) — в рабочей директории и области подготовленных файлов есть более новая версия по сравнению с хранящейся в HEAD (готов к коммиту).
4. Без изменений — одна версия файла во всех разделах, т. е. в последнем коммите содержится актуальная версия.
![Файловая система](%D0%BA%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B0.webp)
Git отслеживает файлы в трёх основных разделах:
* рабочая директория (файловая система вашего компьютера);
* область подготовленных файлов (staging area, хранит содержание следующего коммита);
* HEAD (последний коммит в репозитории).
Все основные команды по работе с файлами сводятся к пониманию того, как Git управляет этими тремя разделами. Существует распространённое заблуждение, что область подготовленных файлов только хранит изменения. Лучше думать об этих трёх разделах как об отдельных файловых системах, каждая из которых содержит свои копии файлов.
## Работа с ветками 
Ветвление — это возможность работать над разными версиями проекта: вместо одного списка с упорядоченными коммитами история будет расходиться в определённых точках. Каждая ветвь содержит легковесный указатель HEAD на последний коммит, что позволяет без лишних затрат создать много веток. Ветка по умолчанию называется master, но лучше назвать её в соответствии с разрабатываемой в ней функциональностью.

Команды:

* git branch <имя ветки> — создаёт новую ветку с HEAD, указывающим на HEAD. Если не передать аргумент <имя ветки>, то команда выведет список всех локальных веток;
* git checkout <имя ветки> — переключается на эту ветку. Можно передать опцию -b, чтобы создать новую ветку перед переключением;
* git branch -d <имя ветки> — удаляет ветку.
## Продвинутое использование
**Интерактивная подготовка**
1234123412341234
Вы можете с удобством управлять областью подготовленных файлов (например при фиксации нескольких небольших коммитов вместо одного большого) с помощью интерактивной консоли, которую можно запустить с git add -i. В ней есть 8 команд:

* status — показывает для каждого файла краткое описание того, что (не)подготовлено;
* update — подготавливает отслеживаемые файлы;
* revert — убрать один или несколько файлов из подготовленной области;
* add untracked — подготавливает неотслеживаемый файл;
* patch — подготавливает только часть файла (полезно, когда вы, например, изменили несколько функций, но хотите разбить изменения на несколько коммитов). После выбора файла вам будут показаны его фрагменты и представлены возможные команды: Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]?. Можно ввести ?, чтобы узнать, что делает каждая команда;
* diff — показывает список подготовленных файлов и позволяет посмотреть изменения для каждого из них;
* quit — выходит из интерактивной консоли;
* help — показывает краткое описание каждой команды.

Символ * рядом с файлом означает, что команда изменит его статус (подготовлен/неподготовлен в зависимости от того, происходит ли обновление или откат). Если нажать Enter, не введя ничего ни в одном из под-меню команды, то все файлы перейдут в (не)подготовленное состояние. Создание патчей доступно в интерактивной консоли и через команду git add -p.

## Работа с удаленными репозиториями
* **git clone**

Клонирование репозитория осуществляется командой git clone <url>.
* **git fetch**

Команда *git fetch* связывается с удалённым репозиторием и забирает из него все изменения, которых у вас пока нет и сохраняет их локально.
* **git pull**

Команда *git pull* работает как комбинация команд git fetch и git merge, т. е. Git вначале забирает изменения из указанного удалённого репозитория, а затем пытается слить их с текущей веткой.

* **git push**

Команда *git push* используется для установления связи с удалённым репозиторием, вычисления локальных изменений отсутствующих в нём, и собственно их передачи в вышеупомянутый репозиторий. Этой команде нужно право на запись в репозиторий, поэтому она использует аутентификацию.
