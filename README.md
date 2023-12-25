Git
git version

$ git config --global user.name "ваше имя или ник латиницей в кавычках" 
$ git config --global user.email ваша электронная почта 

$ cat ~/.gitconfig

git init - сделать папку гит-репозиторием. Перед командой нужно переместиться в нее с помощью cd.
Чтобы разгитить папку, нужно  удалить скрытую подпапку .git:
cd <папка с репозиторием> # перешли в папку
rm -rf .git # удалили подпапку .git
git status - показать текущее состояние репозитория
git add - подготовить файлы к сохранению (запомнить). 
git add --all - все файлы, git add todo.txt - по одному, git add . - добавить всю текущую папку.
git commit - сохранить изменения. Гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться».
git commit -m 'Мой первый коммит!' - присваивает коммиту комментарий. Обычно в таком сообщении поясняется, в чём именно состояли изменения.
git log - посмотреть историю коммитов

Проверка наличия SSH-ключа.
cd ~ # перешли в домашнюю директорию
ls -la .ssh/ # вывели список созданных ключей 
Генерация ssh-пары:
ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"  ИЛИ
ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
Указать место хранения ключей, если дом.директория - энтер.
Кодовая фраза (passphrase). Если оставить поле пустым, то снова энтер. И затем еще раз энтер для подтверждения.
ls -a ~/.ssh - проверить, что ключи сгенерировались (выведет два файла .pub и без расширения (приватный)).

Привязываем SSH-ключ к GitHub.
clip < ~/.ssh/id_ed25519.pub - скопировать содержимое ключа в буфер обмена.
Либо выведите содержимое файла с помощью cat ~/.ssh/id_ed25519.pub и скопируйте вывод в буфер обмена из консоли.
На гитхаб справа вверху кликаем, переходим в Сеттинг, слева ssh, нажимем New ssh key, назваем, копируем свой ключ из буфера обмена.
ssh -T git@github.com - проверяем правильность ключа. После предупреждения вводим yes.

Привязать удалённый репозиторий к локальному.
Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL.
cd ~/dev/first-project - перейти в каталог локального репозитория. (В моем случае путь без dev.)
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git - Привязать удалённый репозиторий к локальному. Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.
git remote -v - Убедиться, что репозитории связаны.

Синхронизируем локальный и удалённый репозитории.
git push - Отправить изменения на удалённый репозиторий.
git push -u origin main # Если команда приведёт к ошибке, попробуйте заменить main на master. В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой.
При взаимодействии с удалёнными репозиториями Git выводит в консоль отладочную информацию: количество объектов (файлов), которые отправляются на сервер, информацию о прогрессе сжатия и записи и так далее.
Если вы указывали кодовую фразу при настройке SSH-ключей, её нужно будет ввести.
Зайдите в репозиторий first-project на GitHub. Вы увидите, что в репозитории появились файлы с изменениями.
В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push