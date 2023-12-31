# Задание
- Составьте постмортем на основе реального сбоя системы GitHub в 2018 году.
- Информацию о сбое можно изучить по ссылкам ниже:
- краткое описание на русском языке [https://habr.com/ru/articles/427301/]
- развёрнутое описание на английском языке [https://github.blog/2018-10-30-oct21-post-incident-analysis/]
## Ответ
- "Постмортем" - это термин, который используется в сфере информационных технологий, чтобы обозначить анализ и обсуждение причин и последствий сбоя или инцидента после его завершения. Он является частью процесса управления инцидентами и направлен на предотвращение подобных проблем в будущем.
В контексте сбоя системы GitHub в 2018 году "постмортем" означает, что команда GitHub провела анализ инцидента, определила его причины, выработала рекомендации по устранению проблемы и предложила улучшения для предотвращения подобных инцидентов в будущем.

### Постмортем по инциденту на GitHub октябрь 2018 года
- Incident Overview (Обзор событий): На прошлой неделе в GitHub произошел серьезный инцидент, который привел к деградации сервиса в течение 24 часов и 11 минут. Инцидент был вызван работой по техническому обслуживанию сети, что привело к потере связи между сетевым хабом на восточном побережье США и основным центром обработки данных на восточном побережье. Это вызвало цепочку событий, затрагивающих несколько внутренних систем и приводящих к отображению устаревшей и несогласованной информации. Несмотря на это, пользовательские данные не пострадали, однако в настоящее время продолжается ручное согласование нескольких секунд записей в базе данных.
- Background(Краткая информация) : Основная часть сервисов GitHub, доступных пользователям, размещается в собственных центрах обработки данных. Однако, несмотря на слои резервирования, кратковременное отсутствие связи между центрами обработки данных вызвало серию проблем.
- Хронология событий:
  - 21 октября 2018 года, 22:52 UTC: Работы по рутинному техническому обслуживанию вызывают сетевую разделенность, что приводит к деактивации оркестратора для инициирования отказа от выбора лидерства. Узлы оркестратора на восточном и западном побережьях устанавливают кворум и перенаправляют записи на West Coast.
  - 21 октября 2018 года, 23:07 UTC: Инженеры выявляют неожиданные состояния баз данных, уровень оповещений растет. Ситуация переходит в активный инцидент.
  - 21 октября 2018 года, 23:13 UTC: Инженеры из команды баз данных начинают ручную конфигурацию баз данных на восточном побережье для восстановления кластеров.
  - 22 октября 2018 года, 00:05 UTC: Разрабатывается план восстановления из резервных копий, синхронизации реплик и восстановления обычной работы. Процесс занимает несколько часов из-за передачи данных из удаленного хранилища.
  - 22 октября 2018 года, 11:12 UTC: Восстанавливаются основные базы данных на восточном побережье, улучшая производительность, но задержка реплик приводит к несогласованности данных для пользователей.
  - 22 октября 2018 года, 16:24 UTC: Производится переключение на исходную топологию для решения проблем с задержкой и доступностью.
  - 22 октября 2018 года, 23:03 UTC: Все непрошедшие  webhooks и сборки страниц обработаны, целостность системы подтверждена, статус сайта обновлен на зеленый.

- Next Steps (Планы на будущее):
  - Разрешение несогласованности данных: Проводится анализ для согласования записей, не реплицированных на  West Coast. Цель - сохранить целостность и точность данных пользователей.

- Communication (Коммуникация): GitHub признает недостатки в предоставлении точных оценок и обещает улучшить коммуникацию в будущем.
- Technical Initiatives (Технические инициативы): Идентифицирован ряд технических инициатив, включая корректировку конфигурации оркестратора, внедрение нового механизма отчетности о статусе и ускорение миграции в активную/активную/активную конструкцию центра обработки данных.
- Organizational Initiatives (Организационные инициативы): Инцидент провоцирует изменение подхода к надежности сайта, включая внедрение систематической практики проверки сценариев сбоя до их воздействия на пользователей.
- Conclusion (Заключение): GitHub признает влияние инцидента на пользователей и обещает проанализировать событие для обнаружения возможностей улучшения. Компания продолжает свою работу над обеспечением надежности платформы и заслуживания доверия своего сообщества.

