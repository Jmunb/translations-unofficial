.. _`Network Dashboard`: https://dashboard.testnet.concordium.com/
.. _Discord: https://discord.gg/xWmQ5tp

.. _run-a-node:

==========
Запускаем узел (ноду)
==========

.. contents::
   :local:
   :backlinks: none

Из этого руководства вы узнаете, как создать на своем персональном компьютере узел (ноду),
который будет участвовать в работе сети Concordium. Это значит, что вы будете получать
блоки и осуществлять транзакции с другими узлами, а также распространять данные о блоках
и транзакциях на другие узлы сети Concordium.

-  запустить узел Concordium
-  наблюдать за ним на сетевой панели инструментов
-  запросить состояние блокчейна Concordium напрямую со своего компьютера

Для того, чтобы создать узел, вам не нужно создавать счет.

Прежде, чем вы начнете
================

Прежде, чем создать узел в сети Concordium вам необходимо:

1. Установить и запустить Docker.

   -  В *Linux*, разрешить запуск Docker от обычного пользователя.

2. Загрузите и разархивируйте следующее ПО :ref:`concordium-node-and-client-download`.

Обновление с более ранней версии Open Testnet
===============================================

Для того, чтобы обновить текущее программное обеспечение Concordium для работы Open Testnet 4:

-  Следуйте вышеописанным шагам по ссылке :ref:`download<downloads>` , чтобы получить самую актуальную версию ПО Concordium.

-  Запустите исполняемый файл ``concordium-node-reset-data`` из распакованного архива.

   -  Для пользователей *Mac*: при первом запуске инструмента щелкните
      правой кнопкой мыши по файлу ``concordium-node-reset-data`` и нажмите
      **Открыть**. На экране появится сообщение, что программное обеспечение
      принадлежит неизвестному разработчику. Снова нажмите на **Открыть**.
   -  Для пользователей *Windows*: при первом запуске инструмента дважды
      кликните по файлу ``concordium-node-reset-data``. На экране появится
      сообщение, что программное обеспечение принадлежит неизвестному разработчику.
      Выберите **Еще** → **Все равно продолжить**.

-  Появится вопрос:

      *Хотите ли вы также удалить сохраненные ключи?*


   Счета, которые были созданы для предыдущих версий, больше не действуют в Open Testnet 3.
   Поэтому если вы сохранили учетные записи из предыдущих версий, мы рекомендуем нажать **y** для того,
   чтобы удалить ключи от всех аккаунтов.

.. _running-a-node:

Запускаем узел
==============

Чтобы запустить клиент, который присоединится к Open Testnet, выполните следующие действия:

1. Откройте исполняемый файл ``concordium-node`` из распакованного архива.

-  Для пользователей *Mac*: при первом открытии инструмента кликните правой кнопкой
   мыши по двоичному файлу ``concordium-node`` и выберите **Открыть**. На экране появится
   сообщение, что программное обеспечение принадлежит неизвестному разработчику. Снова нажмите на **Открыть**.
-  Для пользователей *Windows*: при первом запуске инструмента дважды кликните по по двоичному файлу ``concordium-node``.
   На экране появится сообщение, что программное обеспечение принадлежит неизвестному разработчику. Выберите **Еще** → **Все
   равно продолжить**.
-  При *перезагрузке* узла рассмотрите возможность использования параметра ``--no-block-state-import``. Благодаря этому вы
   загрузите только актуальные обновления блокчейна Concordium, которые появились пока узел был не активен, что может
   ускорить сам процесс запуска.

2. Введите название для своего узла. Оно будет отображаться на общей панели инструментов.

3. Если инструмент запускался ранее, появится вопрос, хотите ли вы удалить базу данных локального узла перед запуском.
   Нажатием **y** вы удалите а затем пересоздадите информацию о состоянии блокчейна Concordium, которая хранилась на вашем компьютере.
   Обратите внимание, что удаление базы данных локального узла приведет к тому, что вам потребуется немного больше времени,
   чтобы установить соединение с сетью Concordium.

Теперь клиент загрузит образ Concordium Client и запустит его в Docker. После запуска клиента он будет генерировать информацию о работе узла.

Отображение узла на панели инструментов
=================================

После запуска ``concordium-node`` вы сможете:

-  увидеть свой узел в `Сетевой панели инструментов`_
-  :ref:`query<testnet-query-node>` информацию о блоках, транзакциях и счетах

Сетевая панель инструментов
-----------------

Клиенту потребуется некоторое время, чтобы обновить статус блокчейна Concordium.
Это подразумевает, например, загрузку информацию обо всех блоках в цепочке.

Среди прочего на `Сетевой панели инструментов`_ отображается сколько времени потребуется вашему узлу,
чтобы актуализировать данные о цепочке. Для этого вы можете сравнить значение **Длины** узла (количество блоков,
полученных вашим узлом) со значением **Длины цепочки** (количество блоков в самой длинной цепочке в сети), которое
отображается в верхней части панели инструментов.


Enabling inbound connections
============================

Если вы запускаете свой узел вместе с фаерволом или используете домашний роутер,
то тогда вы, вероятно, сможете только подключаться к другим узлам.
Другие узлы не смогут инициировать соединение с вашей нодой.
Так и должно быть, ваш узел сможет полноценно участвовать в сети Concordium.
Он сможет отправлять транзакции и  :ref:`if so configured<become-a-baker>`,
чтобы майнить и финализировать процесс.

Однако вы можете качественно улучшить участие вашего узла в сети путем создания входящий подключений.
По умолчанию ``concordium-node`` проверяет соединение с портом ``8888`` для установки входящих подключений.
В зависимости от конфигурации вашей сети и платформы вам потребуется либо осуществить переадресацию внешнего
порта на порт ``8888`` роутера, либо открыть его на вашем файерволе, либо сделать и то, и другое. Детали того,
как это сделать, будут зависеть от вашех настроек.

Настройка портов
-----------------

Узел прослушивает четыре порта, которые можно настроить, указав соответствующие аргументы командной строки при запуске узла.
Узел использует следующие порты:

-  8888, порт для одноранговой сети, который можно настроить с помощью
   ``--listen-node-port``

-  8082, порт, используемый подпрограммным обеспечением, который может быть установлен с помощью ``--listen-middleware-port``
-  10000, порт gRPC, который можно настроить с помощью ``--listen-grpc-port``

При изменении мапинга Докер контейнер должен быть остановлен (:ref:`stop-a-node`), перезагружен и запущен вновь.
Для перезагрузки контейнера можно использовать ``concordium-node-reset-data`` или запустить ``docker rm concordium-client`` в терминале.

Мы *настоятельно рекомендуем*, чтобы все внешние подключения на вашем файерволе были настроены через порт 8888 (порт одноранговой сети).
Потому что, если кто-то получит доступ к другим вашим портам, то он сможет получить контроль над вашим узлом или данными счетов,
сохраненных на узле.

.. _stop-a-node:

Остановка узла
=================

Для того, чтобы остановить узел, нажмите **CTRL+c** и дождитесь полного завершения работы узла.

Если случайно вы закрыли окно до полного завершения работы клиента, оно продолжит работать в фоновом режиме в Docker.
В таком случае используйте бинарный файл ``concordium-node-stop`` также как вы делали при запуске исполняемого файла ``concordium-node``.

Служба поддержки и обратная связь
==================

Информацию из журнала вашего узла можно получить используя инструмент concordium-node-retrieve-logs.
Он сохраняет текущие данные в файл. Кроме того, при наличии разрешения он также будет сохранять информацию
о программах, запущенных в настоящее время.

Вы можете отправлять свои логи, системные данные, вопросы и комментарии на `testnet@concordium.com`_.
Вы также можете обратиться в наш `Discord`_ или на :ref:`страницу устранения неполадок<troubleshooting-and-known-issues>`.

.. _Discord: https://discord.gg/xWmQ5tp
.. _`testnet@concordium.com`: mailto:testnet@concordium.com
