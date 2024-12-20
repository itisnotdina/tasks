
<!--
- указывала абсолютные ссылки на документацию Selectel, потому что доступа делать относительные у меня нет)
- использовала дефолтные адмонишны и инфобоксы докзавра, правда рендериться не будут(
-
-->


## Заказ сервера в панели управления

Для того чтобы заказать облачный сервер, зайдите в панель управления. Здесь вы можете создать сервер с необходимыми конфигурациями.

:::note

Убедитесь, что у вас [пополнен баланс](https://docs.selectel.ru/control-panel-actions/balance-and-payments/manage/top-up-balance/), чтобы создать сервер сразу. Иначе после настроек вам нужно будет выполнить дополнительные шаги для его пополения.

:::

1. В меню навигации перейдите в раздел **Облачная платформа → Серверы**.
2. Нажмите **Создать сервер**.
3. Задайте необходимые настройки сервера.
4. Проверьте настройки и цену сконфигурированного сервера и нажмите **Создать сервер** в окне **Цена**.

### Имя и расположение
---

| Поле   | Описание                                                                                                                                  |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Имя    | Введите имя сервера. Оно будет установлено как имя хоста в операционной системе.                                                          |
| Регион | Выберите регион, в котором будет создан сервер. От выбранного региона зависит список доступных конфигураций сервера и стоимость ресурсов. |
| Пул    | Выберите сегмент пула, в котором будет создан сервер. После создания сервера изменить сегмент пула нельзя.                                |

<!---
Почему, кстати, поле называется пулом, если мы по факту выбираем только сегмент?
--->

### Источник
---

Нажмите на имя источника по умолчанию. В появившемся модальном окне выберите источник, из которого будет создан сервер.

<Tabs>

<TabItem value="ready-made-images" label="Готовые образы" default>

Вы можете создать сервер из готового образа с предустановленной и настроенной операционной системой. Для этого:

1. Отфильтруйте образы по нужной операционной системе и их типу:
    - **Актуальные** – поддерживаемые на текущий момент образы.
    - **Архивные** – образы, обновления которых больше не поддерживаются.

<!---
По объяснению типов - это просто мои предположения, я бы уточнила еще в чем принципиальная разница и почему мы даем возможность выбирать архивные образы.
--->

2. Нажмите на карточку [образа](https://docs.selectel.ru/cloud/servers/images/about-images/#default-images) с подходящими минимальными требования к ресурсам и нажмите **Выбрать**.

:::tip

Готовые образы доступны во всех сегментах пула.

:::

</TabItem>

<TabItem value="apps" label="Приложения">

Вы можете создать сервер с преднастроенными приложениями. Для этого:

1. Отфильтруйте приложения по нужной категории и их типу:
    - **Актуальные** – поддерживаемые на текущий момент приложения.
    - **Архивные** – приложения, обновления которых больше не поддерживаются.

<!---
Опять же, это просто мои предположения, я бы уточнила еще в чем принципиальная разница и почему мы даем возможность выбирать архивные приложения.
--->

2. Нажмите на карточку [приложения](https://docs.selectel.ru/cloud/servers/applications/about-applications/) с подходящими минимальными требования к ресурсам и нажмите **Выбрать**.

:::tip

Приложения доступны во всех сегментах пула.

:::

</TabItem>

<TabItem value="my-images" label="Мои образы">

При создании сервера вы можете использовать собственный образ, который [ранее загрузили](https://docs.selectel.ru/cloud/servers/images/create-image/) в хранилище.

<!---
тут я не смогла загрузить свой образ, чтобы посмотреть, как выглядит вкладка и есть ли фильтрация, поэтому инструкции нет.
--->

:::caution

Образ должен находиться в одном сегменте пула с сервером.

:::

</TabItem>

<TabItem value="disks" label="Диски">

Вы можете создать сервер из сетевого диска.Для этого:

1. Отфильтруйте диск по [необходимым типам](https://docs.selectel.ru/cloud/servers/volumes/about-network-volumes/).
2. Нажмите на карточку [диска](https://docs.selectel.ru/cloud/servers/applications/about-applications/) и нажмите **Выбрать**.


:::caution

Диск должен находиться в одном сегменте пула с сервером.

:::

</TabItem>

<TabItem value="snapshots" label="Снапшоты">

Вы можете создать сервер из снапшота сетевого диска. Для этого:

1. Отфильтруйте снапшоты по дате и диску.
2. Нажмите карточку снапшота и нажмите **Выбрать**.

:::caution

Снапшот должен находиться в одном сегменте пула с сервером.

:::

</TabItem>

</Tabs>


### Конфигурация
---

В конфигурациях используются разные процессоры в зависимости от линейки и сегмента пула. После создания сервера вы можете изменить конфигурацию.

:::note

Объем оперативной памяти, который выделяется серверу, может быть меньше указанного в конфигурации – ядро операционной системы резервирует часть оперативной памяти в зависимости от версии ядра и дистрибутива.

Выделенный объем на сервере можно проверить с помощью команды `sudo dmesg | grep Memory`.

:::


#### Фиксированная

Фиксированная конфигурация представлена в виде нескольких линеек с разными техническими характеристиками, в которых зафиксировано соотношение ресурсов.

Откройте вкладку с нужной [линейкой](https://docs.selectel.ru/cloud/servers/create/configurations/) и выберите необходимые технические характеристики.

#### Произвольная

В произвольной конфигурации вы самостоятельно указываете vCPU, RAM, размер локального диска и, при необходимости, GPU.

|Поле|Описание|
|--|--|
|Локальный SSD NVMe диск|Отметьте чекбокс, чтобы выбрать локальный диск в качестве загрузочного диска сервера. Если в качестве загрузочного диска вам нужно установить сетевой диск, не отмечайте чекбокс.|
|vCPU|Укажите нужное количество vCPU.|
|RAM|Укажите необходимый размер RAM в МБ или ГБ.|
|Локальный диск|Укажите необходимый размер локального диска в ГБ или ТБ. Поле появляется, когда отмечен чекбокс **Локальный SSD NVMe диск**.|
|Тип GPU| Выберите тип GPU. Поле появляется после нажатия на **Добавить GPU**. Если отмечен чекбокс **Локальный SSD NVMe диск**, вы не сможете настроить GPU. |
|Количество|Укажите количество GPU. Поле появляется после нажатия на **Добавить GPU**. Если отмечен чекбокс **Локальный SSD NVMe диск**, вы не сможете настроить GPU.|

### Диски
---

Для сервера вы можете выбрать тип сетевого загрузочного диска, настроить его размер, а также добавить дополнительные диски при необходимости.

| Поле      | Описание                                                |
|-----------|---------------------------------------------------------|
| Тип диска | Выберите тип сетевого диска.                            |
| Размер    | Укажите размер сетевого загрузочного диска в ГБ или ТБ. |

:::caution

Учитывайте лимиты сетевых дисков на максимальный размер.

:::

- Чтобы добавить другой дополнительный диск, нажмите **Добавить**.
- Чтобы удалить один из добавленных дисков, нажмите ![](./img/trash_icon.svg).

После создания сервера можно отключить от него дополнительные диски или подключить новые.

### Сеть
---

Выберите подсеть, к которой будет подключен сервер и заполните IP в поле **Приватный/Публичный IP**. Название поля зависит от настроек подсети.

Чтобы создать новую подсеть, выберите ее тип из доступных:

- **Приватная** – подсеть без доступа из интернета.

    Вы можете изменить сетевые настройки по умолчанию:

    | Поле                         | Описание                                                                                                                                       |
    |------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
    | CIDR подсети                 | Укажите CIDR подсети.                                                                                                                          |
    | DHCP                         | Включите опцию сетевого протокола, чтобы сетевым устройства автоматически получали IP-адрес и другие параметры, необходимые для работы в сети. |
    | Шлюз                         | Укажите IP-адрес шлюза по умолчанию.                                                                                                           |
    | Подсеть будет создана в сети | Выберите **Новая сеть**.                                                                                                                       |
    | Имя сети                     | Введите имя сети.                                                                                                                              |

- **Приватная + 1 публичный IP** – приватная подсеть со статическим публичным IP-адресом. По умолчанию в подсети из интернета будет доступен только сервер, к которому подключается публичный IP-адрес.

    Автоматически будут созданы приватная сеть **nat**, приватная подсеть, роутер **router-nat** и публичный IP-адрес.

- **Публичная** – подсеть, в которой все адреса доступны из интернета.

    |Поле|Описание|
    |--|--|
    |Размер подсети|Выберите количество IP-адресов в подсети.|


### Доступ
----

Разместите на сервере SSH-ключ проекта для безопасного подключения.

| Поле             | Описание                                                                                                                |
|------------------|-------------------------------------------------------------------------------------------------------------------------|
| SSH-ключ         | Нажмите **Добавить SSH-ключ**, введите имя ключа, вставьте публичный SSH-ключ в формате OpenSSH и нажмите **Добавить**. Если SSH-ключ добавлен в облачную платформу, в поле SSH-ключ выберите существующий ключ. |
| Пароль для «root»|Пароль пользователя root с неограниченными правами на все действия над системой. Сохраните пароль в безопасном месте и не передавайте в открытом виде.|

:::caution

SSH-ключ доступен только в том пуле, в котором он размещен.

:::

### Дополнительные настройки
---

Если вы планируете создать несколько серверов и хотите повысить отказоустойчивость инфраструктуры, добавьте сервер в группу размещения и укажите необходимые теги.

Чтобы добавить группу, нажмите **Создать группу** и заполните поля секции.

| Поле                        | Описание                                                       |
|-----------------------------|----------------------------------------------------------------|
| Группа размещения           | Выберите созданную ранее группу размещения или создайте новую. |
| Имя группы                  | Укажите имя новой группы.                                      |
| Размещение на разных хостах | Выберите политику размещения на разных хостах. Доступные опции: <ul><li>**Желательно** – cистема постарается разместить серверы на разных хостах. Если при создании сервера не будет подходящего хоста, он будет создан на том же хосте. </li><li>**Обязательно** – cерверы в группе обязательно располагаются на разных хостах. Если при создании сервера не будет подходящего хоста, сервер не будет создан.</li></ul> Поле появляется только при создании новой группы.|
| Теги                        | Добавьте тег для сервера для дополнительной информации, чтобы фильтровать серверы в списке. Автоматически добавляются теги операционной системы и конфигурации.|


<!---
1. про группы размещения немного не поняла: если у нас уже сущестует группа, она будет отображаться в выпадающем списке, когда мы нажимаем на кнопку Создать группу?

2. `Опционально: чтобы создать прерываемый сервер, отметьте чекбокс Прерываемый сервер.`
не нашла этот чекбокс, может не выбрала необходимую опцию. убрала из описания, уточнила бы у разработчика.
-->

### Автоматизация
---

В поле **User data** вы можете указать скрипт, который выполнится с помощью агента [cloud-init](https://cloudinit.readthedocs.io/en/latest/index.html) при первом запуске операционной системы.

Добавить скрипт можно одним из доступных способов:

- во вкладке **Текст**, с указанием скрипта в поле.
- во вкладке **Файл**, с загрузкой файла со скриптом.

Примеры скриптов и поддерживаемые форматы можно посмотреть в инструкции [User data](https://docs.selectel.ru/cloud/servers/manage/user-data).
