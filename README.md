# Сборник скриптов для CoD4 сервера на Linux + bigbrotherbot.
* ggc.pl - отвечает за обновление базы блокировки с сайта ggc-stream.net. Использует технологию PunkBuster, не требует регистрации сервера на ggc-stream.net.
Настройки(в файле ggc.pl,переменные отвечают):
 - `$_gname` - аббревиатура игры,которая используется на сайте ggc-stream.net. На основе этого значения осуществляется поиск xml Feed.По умолчанию = cod4.
 - `$_pref` - префикс к стандартному тексту исключения, не обязателен. По умолчанию = by GGC-Stream.
 - `$_white` - причина,которую программа игнорирует при добавлении пользователя в базу блокировки. По умолчанию = MD5TOOL.
 - `$_fname` - файл,куда будет вестись запись. По умолчанию = cod4.dat.
 - `$_dirr` - путь к папке PunkBuster. По умолчанию = /root/shared/pb.
* pbss.pl - отвечает за сбор информации о pbss и упорядочивающие в mysql базе.
[Внимание! Требует доработки,возможна потеря подключения к бд через дня 3].
 - `$_dirr` - путь до папки с скриншотами.
 - `$_logname` - название лога для отслеживания ошибок.
 - `$_fname` - название .htm файла, со списком pbss.По умолчанию = pbsvss.htm.
 - `$_maxid` - максимальный id pbss. Состоит из приписки "pb" и 6 значного числа,которое означает максимальное количество pbss на вашем сервере. По умолчанию = pb002000.
 - `$db = DBI->connect("DBI:mysql:bb3_main:","","");` - строка отвечает за подключение к бд, оформляется в виде "$db = DBI->connect("DBI:mysql:Название вашей бд:","Логин","Пароль");".
* votePlugin.(py|xml) - плагин для bigbrotherbot'a,добавляет голосование на смену карты.В файле votePlugin.xml настройки:
 - `<settings name="commands">...</settings>` - список команд плагина.
  - `<set name="...">...</set>` - описание команды, ее имя и уровень с которого ее можно использовать.
 - `<set name="votetimestart">...</set>` - время проведения голосования. По умолчанию = 120 секундам.
 - `<set name="minVoteRatio">...</set>` - минимальное количество голосов "за".
 - `<maps></maps>` - разрешенные карты для голосования.
Новые команды,которые добавляет плагин:


!veto - завершает голосование,очищает количество голосов "за" и "против".
!maprestart - осуществляет быструю перезагрузку карты.
!maplist или !mlist - список карты доступных для голосования.
!votemap или !vm - начать голосование. Синтаксис !votemap map_name.
!votestatus или !vs - статус текущего голосования.
!voteyes или !yes - голосование "за".
!voteno или !no - голосование "против".
