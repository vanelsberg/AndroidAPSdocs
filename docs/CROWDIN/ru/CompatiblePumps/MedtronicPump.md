* * *

orphan: true

* * *

# Помпы Medtronic

Драйвер не работает с новыми моделями, включая все модели, заканчивающиеся на G (530G, 600-серия [630G, 640G, 670G], серия 700-серия [770G, 780G] и т. д.).

Для работы с AAPS подходят следующие комбинации моделей и прошивок:

- 512/712 (любая версия прошивки)
- 515/715 (любая версия прошивки)
- 522/722 (любая версия прошивки)
- 523/723 (прошивка 2.4 или ниже)
- 554/754 версия ЕС (прошивка 2.6A или ниже)
- 554/754 Канадская версия (прошивка 2.7A или ниже)

Проверьте прошивку в соответствии с инструкциями в [OpenAPS документы](https://openaps.readthedocs.io/en/latest/docs/Gear%20Up/pump.html#how-to-check-pump-firmware-check-for-absence-of-pc-connect) и [LoopDocs](https://loopkit.github.io/loopdocs/build/step3/#medtronic-pump-firmware).

## Требования к аппаратному и программному обеспечению

- **Телефон:** Драйвер Medtronic должен работать с любым телефоном на Android, поддерживающим Bluetooth-соединения. **ВАЖНО: Исполнение Bluetooth разное у разных производителей телефонов, поэтому разные модели телефонов ведут себя по-разному. Например, некоторые телефоны по-разному. включают/отключают Bluetooth. Это может повлиять на опыт пользователя, когда AAPS необходимо переподключиться к устройству типа Rileylink.**
- **RileyLink Compatible Device:** Android phones cannot communicate to Medtronic pumps without a separate device to handle communications. Это устройство соединяется с телефоном через Bluetooth и с помпой через совместимое радио соединение. Первое подобное устройство называлось Rileylink, но в настоящее время доступны и другие варианты с дополнительным функционалом.
    
    - Rileylink можно заказать на [getrileylink.org](https://getrileylink.org/product/rileylink916)
    - Orangelink можно заказать на [getrileylink.org](https://getrileylink.org/product/orangelink)
    - Emalink (несколько вариантов модели) доступно на сайте [github.com](https://github.com/sks01/EmaLink)
    - Gnarl (требуется немного самостоятельной работы) подробности на [github.com](https://github.com/ecc1/gnarl)

A comparison chart for the various Rileylink compatible devices can be found at [getrileylink.org](https://getrileylink.org/rileylink-compatible-hardware-comparison-chart)

(MedtronicPump-configuration-of-the-pump)=

## Настройка помпы

Для удаленной отправки команд на помпу необходимо настроить следующие параметры. Шаги, необходимые для каждого изменения на Medtronic 715 показаны в скобках для каждого параметра. Точные шаги могут слегка отличаться в зависимости от типа помпы и/или версии прошивки.

- **Включить удаленный режим на помпе** (На помпе нажмите ACT\---Utilities (Утилиты) --> Remote Optiond (Опции удаленного режима), выберите "Вкл", и на следующем экране нажмите "Добавить ID" и добавьте любой случайный идентификатор, например 111111). Для того чтобы помпа ожидала удаленной связи, в списке удаленных соединений должен быть по крайней мере один идентификатор.
- **Установить Max Basal** (На помпе нажмите ACT -- Basal, --затем выберите Max Basal Rate(макс скорость базала) Например, установка этого значения в четыре раза выше максимальной стандартной скорости позволит задавать временную скорость базала на 400%. Максимальное допустимое значение помпы составляет 34,9 ед. в час.
- **Установить Max Bolus (максимальный болюс) ** (На помпе нажмите ACT -- Bolus и затем выберите Max Bolus) Это максимальный разовый болюс, который подает помпа. Максимальное разрешенное значение помпы составляет 25 ед.
- **Задайте профиль как STD (стандартный) **. (На помпе нажмите ACT, перейдите в Базал, а затем Select Patterns (выбрать рисунок профиля). Помпе понадобится только один профиль, а AAPS будет управлять различными профилями на телефоне. Другие профили не требуются.
- **Установить тип временной скорости базала Basal Rate type** (На помпе нажмите ACT и перейдите в Basal и затем Temp Basal Type). Выберите Absolute Абсолютный (не в процентах).

## Конфигурация помп Medtronic и телефона /AAPS

- **Не подключайте устройство, совместимое с RileyLink, к меню Bluetooth на телефоне.** Привязка через меню Bluetooth телефона не позволит AAPS видеть совместимое устройство Rileylink при выполнении дальнейших инструкций.
- Отключите автоматический поворот экрана на телефоне. На некоторых устройствах автоматическая вращение экрана приводит к перезапуску сессий Bluetooth, что может вызвать проблемы с помпой Medtronic. 
- Существует два способа настройки помпы Medtronic в AAPS:

1. Использовать мастер установки при первой установке приложения
2. Выбрав значок шестеренки рядом с помпой Medtronic в опции выбора помпы в Конфигураторе

When configuring your Medtronic pump with the setup wizard it is possible that you will be prevented from completing setup because of Bluetooth issues (e.g. you cannot successfully connect to the pump). В этом случае следует выбрать виртуальную помпу, и перейти к опции 2.

![Настройки Medtronic](../images/Medtronic01a.png)

При настройке AAPS для работы с помпой Medtronic следует задать следующие параметры: (см. рисунок выше)

- **Серийный номер помпы**: Находится на задней панели помпы и начинается с SN. You should only enter the 6 numbers shown without any alphabetic characters (e.g. 123456).
- **Pump Type**: Используемая модель помпы (например, 522). 
- **Частота помпы**: Есть два варианта, в зависимости от региона рынка. Проверьте [FAQ](#faq) если не уверены что выбрать): 
    - для США & Канады применяется частота 916 МГц
    - для остального мира - 868 МГц
- **Макс. базал на помпе (ед./ч.)**: Должен соответствоватьпараметрам помпs (см. Конфигурация помпы выше). Опять же эта настройка должна быть тщательно подобрана, так как определяет, какую базу можно задать для AAPS. То есть установить максимальную величину временного базала. Например, установка этого значения в четыре раза выше максимальной стандартной скорости позволит задавать временную скорость базала на 400%. Максимальное допустимое значение помпы составляет 34,9 ед. в час.
- **Макс. Болюс на помпе (ед.)**(в течение часа): Должен соответствовать параметрам помпы (см. Конфигурация помпы выше). Эта настройка должна быть тщательно подобрана, так как определяет, насколько большим может быть болюс, подаваемый с AAPS.
- **Задержка перед подачей болюса (ов)**: Количество секунд перед тем, как команда фактически передается на помпу. Этот период времени позволяет пользователю отменить болюс в случае, если команда подана по ошибке. Невозможно отменить болюс, который выполняется через AAPS. Единственный способ отменить уже начатый болюс - это приостановить помпу вручную, а затем возобновить ее работу.
- **Medtronic Encoding (кодировка Medtronic)**: Определяет, выполняется ли кодировка Medtronic. Выбор аппаратной кодировки (то есть кодировки, определяемой устройством Rileylink) предпочтительнее, так как приводит к меньшему количеству отправляемых данных. Выбор программной кодировки (т.е. осуществляемой AAPS) может помочь в случае частых отключений. Эта настройка игнорируется, если на устройствах Rileylink установлена прошивка версии 0.x.
- **Тип батареи **: Чтобы правильно определить оставшийся уровень заряда батареи, следует выбрать тип используемой батареи AAA. Если выбран вариант кроме простого, AAPS будет отображать оставшийся заряд батареи в процентах. Доступны следующие варианты:
    
    - Не выбрано (Простой вид)
    - Щелочная (Подробный вид)
    - Литиевая (Подробный вид)
    - NiZn (Подробный вид)
    - Никель-металлогидридная (Подробный вид)
- **Отладка болюсов/терапии Bolus/Treatments Debugging**: Выберите Вкл или Выкл в зависимости от потребности.

- **Конфигурация RileyLink Configuration**: Эта опция позволяет вам найти и связать устройство, совместимое с Rileylink. При этом выборе будут показаны устройства, совместимые с Rileylink, и уровень их сигнала.
- **Использование сканирования Scanning** активирует сканирование Bluetooth перед подключением к устройствам RileyLink. Это должно повысить надежность подключения к устройству.
- **Показать уровень заряда батареи OrangeLink/EmaLink/DiaLink** Эта функция поддерживается только на новых устройствах связи, таких как EmaLink или OrangeLink. Значения будут показаны на вкладке Medtronic в AnroidAPS. 
- **Установить нейтральный врем базал**: По умолчанию помпы Medtronic издают сигнал каждый час, когда активна временная базальная скорость. Enabling this option can help reduce the number of beeps heard by interrupting a temporary basal at the hour change in order to suppress the beep.

## Вкладка MEDTRONIC (MDT)

![Вкладка MDT](../images/Medtronic02.png) Когда AAPS сконфигурирован на использование помп Medtronic, в списке вкладок в верхней части экрана появится вкладка MDT. Эта вкладка отображает текущую информацию о статусе помпы наряду с некоторыми действиями Medtronic.

- **Статус RileyLink Status**: Текущий статус подключения телефона к устройству, совместимому с RileyLink. Здесь всегда должно быть Connectel (сопряжено). Любой другой статус требует вмешательства пользователя. 
- **Батарея RileyLink Battery**: Текущий уровень заряда батареи устройства EmaLink или OrangeLink. В зависимости от выбора "Показать уровень заряда батареи, OrangeLink/EmaLink/DiaLink", в меню конфигурации.
- **Статус помпы**: Статус соединения с помпой. Так как помпа не будет соединена постоянно, здесь в основном показывается пиктограмма сна. Существуют другие возможные статусы, например «Пробуждение», когда AAPS пытается выдать команду или другие возможные команды, такие как «Получить время помпы», "Установить TBR" и т. д.
- **Батарея**: Показывает статус батареи на основе значения, выбранного для типа батареи (Вид заряда батареи) в меню настроек помпы Medtronic. 
- **Last connection**: How long ago the last successful pump connection happened.
- **Last Bolus**: How long ago the last successful bolus was delivered.
- ** Базовая скорость базала**: Основная скорость, с которой подается база на помпе в этот час.
- **Врем базал Temp basal**: Временный базал в настоящее время, может быть и 0 единиц в час.
- ** Резервуар **: Сколько инсулина находится в картридже (обновляется по крайней мере каждый час).
- **Errors ошибки**: строка ошибки, если есть проблемы (в основном показывает, есть ли ошибка в конфигурации).

В нижней части экрана расположены три кнопки:

- **Обновить** для обновления текущего статуса помпы. Ей следует пользоваться только в случае, когда соединение отсутствовало в течение длительного периода, так как потребует полного обновления данных (получение истории, установка времени, получение профиля, получение статуса батареи и т. д.).
- **История помпы**: Показывает журнал помпы (см. [ниже](#pump-history))
- **Статистика RL**: Показать статистику RL (см. [ниже](#rl-status-rileylink-status))

(MedtronicPump-pump-history)=

## Журнал помпы

![Диалоговое окно журнала помпы](../images/Medtronic03.png)

Хронология помпы извлекается каждые 5 минут и сохраняется в памяти. Сохраняются только предыдущие 24 часа истории. The allows for a convenient way to see pump behaviour should that be required. The only items stored are those relevenant to AAPS and will not include a configuration function that has no relevance.

(MedtronicPump-rl-status-rileylink-status)=

## Состояние RL (Состояние RileyLink)

![Состояние RileyLink-Параметры](../images/Medtronic04.png) ![Состояние RileyLink-хронология](../images/Medtronic05.png)

В диалоге состояния RL есть две вкладки:

- ** Параметры **: Показывает параметры RileyLink: Сконфигурированный адрес, Подключенное устройство, Состояние соединения, Ошибка соединения и Версия встроенного ПО (прошивки) RileyLink. Типом устройства всегда является Medtronic Pump, Модель - ваша версия модели, Серийный номер-сконфигурированный серийный номер, Частота помпы- Частота на которой работает связь помпы, Последняя частота-последняя используемая частота связи.
- ** История **: Показывает хронологию связи, элементы с RyleyLink показывают изменения состояния RileyLink, Medtronic показывает, какие команды были отправлены на помпу.

## Действия

При использовании драйвера Medtronic добавляются два дополнительных действия на вкладке Действия:

- ** Пробуждение и настройка **-Если вы видите, что AndroidAPS не связывался с помпой в течение какого-то времени (он должен связываться каждые 5 минут), вы можете нажать кнопку Настройка. AAPS попытается связаться с помпой, пробуя все возможные радиочастоты, используемые помпой. In the event a successful connection is made the successful frequency will be set as the default.
- ** Сброс конфигурации RileyLink **-При перезагрузке RileyLink/GNARL необходимо выполнить эту команду, чтобы переконфигурировать устройство (частота, тип частоты, кодировка).

## Важные Примечания

### Особое внимание при конфигурации NS

AAPS использует серийный номер для синхронизации и серийный номер показывается в NS. Поскольку знание серийно номера старых помп Medtronic может быть использовано для дистанционного управления, следует позаботиться о мерах безопасности сайта NS. См. https://nightscout.github.io/nightscout/security/

### Пользователям OpenAPS

Пользователи OpenAPS должны иметь в виду, что AAPS с Medtronic использует совершенно иную методику, чем OpenAPS. При использовании AAPS основным методом взаимодействия с помпой является работа через телефон. В обычных случаях меню помпы, скорее всего, понадобится только при замене резевуара. Это отличается от OpenAPS, когда по крайней мере некоторые болюсы подаются через кнопки быстрого болюса. В том случае, если помпа используется для ручной подачи болюса, могут возникнуть проблемы, если AAPS пытается подать болюс одновременно с помпой. В таких случаях для предотвращения проблем существуют проверки, однако по возможности их следует избегать.

### Запись логов в файл

In the event you need to troubleshoot your Medtronic pump function select the menu icon in the upper left corner of the screen, select Maintenance and Log Settings. Для устранения неполадок необходимо проверить Pump, PumpComm, PumpBTComm.

### Мониторинг Medtronic

Мониторинг Medtronic в настоящее время не поддерживается.

### Использование помпы вручную

Не следует выполнять болюсы или установку временного базала вручную с помпы. Эти команды должны отправляться через AAPS. В случае подачи команд вручную, между ними следует выдерживать не менее 3 минут, чтобы уменьшить риск возникновения проблем.

### Изменения часового пояса, сезонное время и путешествия с помпой Medtronic и AAPS

AAPS автоматически определит изменения часового пояса и обновит время помпы, когда телефон перейдет на новое время.

Путешествие на восток означает, что потребуется добавлять часы к текущему времени (напр. от GMT+0 до GMT+2) не вызовет никаких проблем, так как время не будет перекрываться (напр один и тот же час не повторится дважды). Однако перелет на запад может привести к возникновению проблем, так как вы фактически переноситесь в обратное время, а это приведет к неправильной оценке IOB.

Проблемы, которые наблюдаются при перелетах на запад, известны разработчикам, которые работают над возможным решением. Дополнительную информацию см. на https://github.com/andyrozman/RileyLinkAAPS/issues/145. На данный момент помните о существовании проблемы и тщательно следите за временем при пересечении часовых поясов.

### Is a GNARL a fully compatible Rileylink compatible device?

Код GNARL полностью поддерживает все функции, используемые драйвером Medtronic в AAPS, что означает, что он полностью совместим. It is important to note that this will require additional work as you will have to source compatible hardware and then load the GNARL code on to the device.

** Примечание автора: ** Обратите внимание, что программное обеспечение GNARL по-прежнему экспериментально и недостаточно протестировано и не должно считаться таким же безопасным как RileyLink.

Часто задаваемые вопросы по помпе Medtronic

## Часто задаваемые вопросы

MedtronicPump -что делать при потере связи с rileylink и/или помпой

### Что делать, если потеряна связь с RileyLink и/или помпой?

Существует несколько вариантов решения проблем с подключением.

- Воспользуйтесь кнопкой "Wake Up and Tune" (Разбудить и настроить) на вкладке ACT, как было описано выше.
- Отключите Bluetooth на вашем телефоне, подождите 10 секунд и включите его снова. Это заставит устройство Rileylink переподключиться к телефону.
- Выполните сброс устройства RileyLink. Используйте кнопку "Сбросить Rileylink Config" на вкладке ACT.
- Другие пользователи обнаружили, что восстановить подключения помогут следующие шаги, когда не помогли другие: 
    1. Перезагрузить телефон
    2. *Во время * перезагрузки перезапустите устройство Rileylink
    3. Откройте AAPS и дайте подключению восстановиться

### Как определить, на какой частоте работает помпа

![Модель помпы](../images/Medtronic06.png)

На задней части помпы вы найдете строку, содержащую номер модели вместе со специальным 3-буквенным кодом. Первые две буквы определяют тип частоты и последняя определяет цвет. Возможны следующие значения частоты:

- NA-Северная Америка (при выборе частоты необходимо выбрать "US & Canada (916 МГц)")
- CA-Канада (для выбора частоты необходимо выбрать "US & Canada (916 МГц)")
- WW- остальные страны (при выборе частоты необходимо выбрать "Worldwide (868 Mhz)")