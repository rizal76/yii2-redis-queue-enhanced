Stomp драйвер
================

Драйвер работает с очередью на базе ActiveMQ.

В приложении должно быть установлено расширение `enqueue/stomp`.

Пример настройки:

```php
return [
    'bootstrap' => [
        'queue', // Компонент регистрирует свои консольные команды 
    ],
    'components' => [
        'queue' => [
            'class' => \flip_id\yii2_queue\stomp\Queue::class,
            'host' => 'localhost',
            'port' => 61613,
            'queueName' => 'queue',
        ],
    ],
];
```

Консоль
-------

Для обработки очереди используются консольные команды.

```sh
yii queue/listen
```

Команда `listen` запускает обработку очереди в режиме демона. Очередь опрашивается непрерывно.
Если добавляются новые задания, то они сразу же извлекаются и выполняются. Способ наиболее эфективен
если запускать команду через [supervisor](worker.md#supervisor) или [systemd](worker.md#systemd).

Для команды `listen` доступны следующие опции:

- `--verbose`, `-v`: состояние обработки заданий выводится в консоль.
- `--isolate`: каждое задание выполняется в отдельном дочернем процессе.
- `--color`: подсветка вывода в режиме `--verbose`.
