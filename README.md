# KFC-project
It is student's project as a part of methodology of software engineering course in ITMO University.

Дальше будет по-русски.

Проект представляет собой ПО для извлечения и агрегирования информации из систем управления проектами: Jira и Trello, а также систем отслеживания ошибок: GitHub Issues, Mantis. Данное ПО потенциально разрабатывается, как часть некоего большого проекта, о котором мы не вправе пока рассказывать.

Приложение строится на микросервисной архитектуре, где будут сервисы-парсеры, сервис-агрегатор, хранилище и управляющий сервис.

Сервисы-парсеры - сервисы для извлечения информации из вышеупомянутых систем (Jira, Trello, GitHub Issues, Mantis) в унифицированном виде. Для каждой системы свой отдельный сервис, который по определенным кредам будет получать доступ к данных (оптимально по хукам) и будет отдавать их агрегатору. В случае с Jira и Trello один проект - один экземпляр сервиса. Экземпляры сервисов будут динамически разворачиваться для каждого нового проекта по мере их добавления.

Хранилище - связка кеша и постоянного хранилища. Кеш будет содержать актуальную информацию из сервисов.
Агрегатор - сервис, который будет служить прослойкой между хранилищем, сервисами и управляющим узлом. Сервисы обращаются в агрегатор, чтобы тот положил информацию в хранилище. Агрегатор отдаёт управляющему узлу данные из хранилища, при этом хитро её агрегируя. За данными агрегатор умеет обращаться только в хранилище, с сервисами он общаться не умеет.

Управляющий узел - некий абстрактный узел, который выходит наружу в виде API. В зависимости от вызовов извне он либо обращается в CI для поднятия нового экземпляра сервиса либо обращается к агрегатору за данными.

CI - CI.

Технологии:
.Net Core C#, Lisp
Tarantool DB, PostgreSQL
Jenkins CI, Docker
