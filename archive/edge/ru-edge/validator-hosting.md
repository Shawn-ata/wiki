---
id: validator-hosting
title: Хостинг валидатора
description: "Требования к хостингу для Polygon Edge"
keywords:
- docs
- polygon
- edge
- hosting
- cloud
- setup
- validator
---

Ниже приведены рекомендации для правильного хостинга узла валидатора в сети Polygon Edge. Просим вас обратить особое внимание на все ниже перечисленные пункты, чтобы убедиться, что ваш валидатор настроен должным образом для обеспечения безопасности, стабильности и эффективности.

## База знаний {#knowledge-base}

Прежде чем запустить узел валидатора, внимательно ознакомьтесь с этим документом.    Ниже приведена другая полезная документация:

- [Установка](get-started/installation)
- [Облачная настройка](get-started/set-up-ibft-on-the-cloud)
- [Команды CLI](get-started/cli-commands)
- [Файл конфигурации сервера](configuration/sample-config)
- [Приватные ключи](configuration/manage-private-keys)
- [Метрика Prometheus](configuration/prometheus-metrics)
- [Диспетчеры секретов](/docs/category/secret-managers)
- [Резервное копирование/восстановление](working-with-node/backup-restore)

## Минимальные системные требования {#minimum-system-requirements}

| Тип | Значение | Под воздействием |
|------|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Процессор | 2 ядра | <ul><li>Количество запросов JSON-RPC</li><li>Размер состояния блокчейна</li><li>Лимит газа для блока</li><li>Время блока</li></ul> |
| ОЗУ | 2 ГБ | <ul><li>Количество запросов JSON-RPC</li><li>Размер состояния блокчейна</li><li>Лимит газа для блока</li></ul> |
| Диск | <ul><li>Корневой раздел 10 ГБ</li><li>Корневой раздел 30 ГБ с LVM для расширения диска</li></ul> | <ul><li>Размер состояния блокчейна</li></ul> |


## Конфигурация сервиса {#service-configuration}

Двоичный файл `polygon-edge` должен запускаться как системная служба автоматически при установления сетевого соединения и иметь функции запуска/остановки/перезапуска . Рекомендуем использовать диспетчер служб, например `systemd.`

Пример `systemd`файла конфигурации системы:
```
[Unit]
Description=Polygon Edge Server
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=10
User=ubuntu
ExecStart=/usr/local/bin/polygon-edge server --config /home/ubuntu/polygon/config.yaml

[Install]
WantedBy=multi-user.target
```

### Двоичный файл {#binary}

В производственных рабочих нагрузках `polygon-edge` двоичный файл должен быть развернут только из предварительно созданных на GitHub двоичных файлах релиза, а не компиляцией его вручную.:::info
Компилируя вручную ветвь GitHub `develop`, вы можете внести серьезные изменения в вашу среду.    Поэтому рекомендуется развертывать двоичный файл Polygon Edge исключительно из релизов, поскольку он будет содержать информацию о серьезных изменениях и о том, как их исправить.  
:::

Полный обзор метода установки можно посмотреть в разделе [Установка](/docs/edge/get-started/installation).

### Хранение данных {#data-storage}

`data/`Папка, содержащая все состояния блокчейна, должна быть смонтирована на выделенном диске/томе, что позволяет автоматически создавать резервные копии диска, расширять том и, по желанию, устанавливать диск/том на другой экземпляр в случае сбоя.


### Файлы журнала {#log-files}

Файлы журнала необходимо ежедневно ротировать (при помощи такого инструмента: `logrotate`).:::warning
Если конфигурация настроена без ротации журналов, файлы журнала могут использовать все доступное дисковое пространство, что может нарушить время работы валидатора.
:::

Пример `logrotate` конфигурации:
```
/home/ubuntu/polygon/logs/node.log
{
        rotate 7
        daily
        missingok
        notifempty
        compress
        prerotate
                /usr/bin/systemctl stop polygon-edge.service
        endscript
        postrotate
                /usr/bin/systemctl start polygon-edge.service
        endscript
}
```


Рекомендации по хранению журналов можно найти в разделе [Ведение журналов](#logging) ниже.

### Дополнительные зависимости {#additional-dependencies}

`polygon-edge`статически компилируется, не требуя дополнительных зависимостей от ОС хоста.

## Техническое обслуживание {#maintenance}

Ниже приведены лучшие советы по техническому обслуживанию узла валидатора сети Polygon Edge.

### Резервное копирование {#backup}

Для нодов Polygon Edge рекомендуется проводить два типа процедур резервного копирования.

Мы предлагаем использовать обе процедуры, когда это возможно, при этом резервная копия Polygon Edge всегда остается доступным вариантом.

* ***Резервное копирование тома***:     Ежедневное инкрементальное резервное копирование `data/`тома нода Polygon Edge или полного VM по возможности.


* ***Резервное копирование Polygon Edge***:     Рекомендуется ежедневно выполнять процедуру CRON, которая регулярно создает резервные копии Polygon Edge и перемещает `.dat`файлы в удаленное место или в безопасное облачное хранилище объектов.

Резервное копирование Polygon Edge в идеале не должно совпадать с описанным выше резервным копированием тома.

Инструкции по выполнению резервного копирования Polygon Edge можно найти в разделе [Резервное копирование/восстановление экземпляра нода](working-with-node/backup-restore).

### Ведение журнала {#logging}

Журналы, выводимые нодами Polygon Edge, должны иметь следующие характеристики:
- отправляться во внешнее хранилище данных с возможностью индексирования и поиска;
- иметь срок хранения журнала 30 дней.

Если вы настраиваете валидатор Polygon Edge впервые, рекомендуем запустить нод с опцией `--log-level=DEBUG`, чтобы иметь возможность быстро отладить любые проблемы, с которыми вы можете столкнуться.

:::info
`--log-level=DEBUG`сделает вывод журнала нода максимально подробным.    Журналы отладки резко увеличат размер файл журнала, который необходимо учитывать при настройке решения по ротации журналов.
:::
### Патчи безопасности ОС {#os-security-patches}

Администраторам необходимо следить за тем, чтобы ОС экземпляра валидатора всегда обновлялась с последними патчами не реже одного раза в месяц.

## Метрика {#metrics}

### Системная метрика {#system-metrics}

Администраторам необходимо установить какой-либо монитор для системной метрики (например, Telegraf + InfluxDB + Grafana или сторонний SaaS).

Метрика, которую необходимо мониторить и которая требует настройки уведомлений о тревоге:

| Название метрики | Порог сигнала тревоги |
|-----------------------|-------------------------------|
| Использование процессора (%) | > 90% в течение более 5 минут |
| Использование ОЗУ (%) | > 90% в течение более 5 минут |
| Использование корневого диска | > 90% |
| Использование диска данных | > 90% |

### Метрика валидатора {#validator-metrics}

Администраторам необходимо настроить сбор метрики API Prometheus Polygon Edge, чтобы иметь возможность отслеживать производительность блокчейн-сети.

См. раздел [Метрика Prometheus](configuration/prometheus-metrics) для понимания того, какая метрика подвергается воздействию и как настроить сбор метрики Prometheus.


Особое внимание следует уделить следующей метрике:
- ***Время производства блока***: если время производства блока превышает норму, возможна проблема с сетью
- ***Количество раундов консенсуса***: если имеется более 1 раунда, возможна проблема с набором валидаторов в сети
- ***Количество одноранговых узлов (пиров)***: если количество пиров падает, возможны проблемы с подключением сети

## Безопасность {#security}

Ниже приведены лучшие советы по обеспечению безопасности узла валидатора сети Polygon Edge.

### Сервисы API {#api-services}

- ***JSON-RPC*** — Только сервис API, который должен быть открыт для публики (через балансировщик или напрямую).    Этот API должен быть запущен на всех интерфейсах или на определенном IP-адресе (например: `--json-rpc 0.0.0.0:8545` или `--json-prc 192.168.1.1:8545`).:::info
Поскольку это публично доступный API, рекомендуется установить балансировщик / обратный прокси-сервер для обеспечения безопасности и ограничения скорости.
:::


- ***LibP2P*** — Это API сетевого взаимодействия, который используют ноды для взаимодействия с пирами. Он должен быть запущен на всех интерфейсах или на определенном IP-адресе ( `--libp2p 0.0.0.0:1478`или `--libp2p 192.168.1.1:1478`). Этот API не должен иметь публичный доступ, но он должен быть доступен со всех других нодов.:::info
При запуске на localhost ( `--libp2p 127.0.0.1:1478` ) другие ноды подключиться не смогут.
:::


- ***GRPC*** — Этот API используется только для запуска команд оператора и больше ни для чего. Как таковой он должен работать исключительно на localhost ( `--grpc-address 127.0.0.1:9632`).

### Секреты Polygon Edge {#polygon-edge-secrets}

Секреты Polygon Edge ( `ibft`и `libp2p`) не должны храниться на локальной файловой   системе. Вместо этого следует использовать поддерживаемый [диспетчер секретов](configuration/secret-managers/set-up-aws-ssm).    Хранение секретов на локальной файловой системе следует применять только в непроизводственных средах.

## Обновление {#update}

Ниже приведена желаемая процедура обновления нодов валидатора, описанная в виде пошаговой инструкции.

### Процедура обновления {#update-procedure}

- Загрузите последний двоичный файл Polygon Edge из официальных [релизов](https://github.com/0xPolygon/polygon-edge/releases) GitHub
- Остановить сервис Polygon Edge ( пример: `sudo systemctl stop polygon-edge.service`)
- Замените существующий двоичный файл `polygon-edge` на загруженный файл (Например: `sudo mv polygon-edge /usr/local/bin/`)
- Проверьте при помощи запуска `polygon-edge version`, работает ли правильная версия `polygon-edge` — она должна соответствовать версии релиза
- Проверьте документацию по релизу, есть ли какие-либо шаги для обратной совместимости, которые необходимо сделать перед запуском сервиса `polygon-edge`
- Запустите сервис `polygon-edge` (пример: `sudo systemctl start polygon-edge.service`)
- Наконец, проверьте вывод журнала `polygon-edge` и убедитесь, что все работает без каких-либо журналов `[ERROR]`

:::warning
При выходе нового релиза эта процедура обновления должна быть выполнена на всех нодах, поскольку работающий в настоящее время двоичный файл не совместим с новым релизом.

Это означает, что цепочка должна быть приостановлена на короткий период времени (пока не будут заменены двоичные файлы `polygon-edge`, а сервис — заново запущен) поэтому планируйте соответствующим образом.

Вы можете использовать такие инструменты, как **[Ansible](https://www.ansible.com/)** , или пользовательский скрипт для эффективного выполнения обновления и минимизации времени простоя цепочки.
:::

## Процедура запуска {#startup-procedure}

Ниже приведен желаемый порядок процедуры запуска валидатора Polygon Edge

- Прочитайте документацию в разделе [База знаний](#knowledge-base)
- Примените последние патчи ОС на узле валидатора
- Загрузите последний двоичный файл `polygon-edge` из официальных [релизов](https://github.com/0xPolygon/polygon-edge/releases) GitHub и поместите его в локальный экземпляр`PATH`
- Запустите один из [диспетчеров секретов](/docs/category/secret-managers) с помощью команды CLI `polygon-edge secrets generate`
- Генерируйте и храните секреты с помощью `polygon-edge secrets init` [команды CLI](/docs/edge/get-started/cli-commands#secrets-init-flags)
- Обратите внимание на значения `NodeID` и `Public key (address)`
- Сгенерируйте файл `genesis.json`, как это описывается в [облачной настройке](get-started/set-up-ibft-on-the-cloud#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators) с помощью `polygon-edge genesis` [команды CLI](/docs/edge/get-started/cli-commands#genesis-flags)
- Сгенерируйте файл конфигурации по умолчанию с помощью `polygon-edge server export` [команды CLI](/docs/edge/configuration/sample-config)
- Отредактируйте файл `default-config.yaml`, чтобы разместить узел проверки локальной среды (пути файлов и т. д.)
- Создайте сервис Polygon Edge (`systemd`или подобный), в котором `polygon-edge`двоичный файл будет запускать сервер из файла `default-config.yaml`
- Запустите сервер Polygon Edge с помощью сервиса (например: `systemctl start polygon-edge`)
- Проверьте вывод журнала `polygon-edge` и убедитесь, что блоки генерируются, а журналы `[ERROR]` отсутствуют
- Проверьте функциональность цепочки с помощью метода JSON-RPC [`eth_chainId`](/docs/edge/api/json-rpc-eth#eth_chainid)