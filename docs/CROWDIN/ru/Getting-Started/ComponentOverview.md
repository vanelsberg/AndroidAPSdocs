# Обзор компонентов

**AAPS** is not just a (self-built) application, it is but one of several modules of your closed loop system. Before deciding for components, it would be a good idea to have a look at the component documentation.

![Components overview](../images/modules.png)

```{note}
**IMPORTANT SAFETY NOTICE**

The foundation of **AAPS** safety features discussed in this documentation is built on the safety features of the hardware used to build your system. For closing an automated insulin dosing loop, it is critically important that you only use an insulin pump and CGM that are tested, fully functioning and approved by the official instances of your country. Внесение аппаратных или программных технических изменений в это оборудование может стать причиной неконтролируемого введения инсулина, что может повлечь опасные последствия для пациента. If you find or get offered broken, modified or self-made insulin pumps or CGM receivers, **do not use** these for creating an **AAPS** system.

Допустимо использовать только оригинальные, сертифицированные производителем расходные материалы, такие как инсулиновые картриджи, инфузионные наборы, пристреливатели к ним и т. п. Использование непроверенных или модифицированных материалов может вызвать неточность мониторинга и ошибки дозировки инсулина. Инсулин опасен при неверной дозировке - не рискуйте жизнью, пользуясь неумело переделанными компонентами.

Last but not least, you must not take SGLT-2 inhibitors (gliflozins) as they incalculably lower blood sugar levels. Сочетание с системой, которая снижает базальную скорость для повышения ГК является особенно опасным, поскольку из-за глифлозинов этот подъем ГК может не произойти и возникнет нехватка инсулина. [More information here](../Getting-Started/PreparingForAaps.md#no-sglt-2-inhibitors).
```

## Необходимые модули

### Хорошо подобранные дозы и коэффициенты для компенсации

Хотя его нельзя сконструировать или купить, это, вероятно, самый недооцениваемый "модуль", существенно важный для системы. Когда алгоритму доверяется управлять диабетом, следует знать правильные настройки, чтобы не допустить серьезных ошибок. Even if you are still missing other modules, you can already verify and adapt your **Profile** in collaboration with your diabetes team.

The **Profile** includes:

- BR (Basal rates): provides background insulin;
- ISF (insulin sensitivity factor): how much your blood glucose level will be reduced by 1 unit of insulin;
- CR (carb ratio): how many grams of carbohydrate are covered by one unit of insulin;
- DIA (duration of insulin action).

Большинство пользователей систем ИПЖ используют циклические суточные величины скорости базала (BR), гормональную чувствительность к инсулину ISF и углеводный коэффициент CR.

More information about your **Profile** [on the dedicated page](../SettingUpAaps/YourAapsProfile.md).

### Телефон

See the dedicated page [Phones](../Getting-Started/Phones.md).

### Инсулиновая помпа

See the dedicated page [Compatible Pumps](../Getting-Started/CompatiblePumps.md).

**Advantages and disadvantages of some pump models**

The Combo, the Insight and the older Medtronic are solid pumps, and loopable. The Combo has the advantage of many more infusion set types to choose from as it has a standard Luer-Lock. And the battery is a default one you can buy at any gas station, 24-hour convenience store and if you really need one, you can steal/borrow it from the remote control in the hotel room ;-).

Однако преимущества помп Dana R/ RS и Dana-i по сравнению с Combo следующие:

- Помпы Dana сопрягается почти с любым телефоном на Android без необходимости перепрошивки на Lineage OS. Если телефон сломается, ему быстро найдется замена, которая работает с Dana... С Combo сложнее. (Ситуация может измениться, когда Android 8.1 станет более популярным)
- Первоначальное сопряжение проходит проще с Dana-i/RS. Но обычно это делается только один раз, так что это свойство важно, если хотите проверить новую функцию на других помпах.
- На данный момент Combo работает с экранным анализом (для обратного инжиниринга). В целом, это неплохо, но этот процесс идет медленно. Для цикла ИПЖ это не имеет значения, так как он работает в фоновом режиме. Still there is much more time you need to be connected so more time when the BT connection might break, which isn't so easy if you walk away from your phone whilst bolusing & cooking.
- Combo вибрирует по завершении временных базалов TBR, Dana вибрирует (или пищит) на микроболюсах SMB. At nighttime, you are likely to be using TBRs more than SMB.  The Dana-i/RS is configurable so that it does neither beep nor vibrate.
- Чтение истории на Dana-i/RS происходит за секунды и позволяет легко заменить телефон в автономном режиме и продолжать работу с появлением новых значений мониторинга CGM.
- All pumps **AAPS** can talk with are waterproof on delivery. Но только помпы Dana также "гарантированно водонепроницаемы" благодаря изолированным отсекам батареи и системы наполнения резервуара.

### Источник данных гликемии

See the dedicated page [Compatible CGMs](../Getting-Started/CompatiblesCgms.md).

### **AAPS**-.apk file

The main component of the system. In order to install the app, you have to build the apk-file yourself first. Instructions are [here](../SettingUpAaps/BuildingAaps.md).

### Reporting server

A reporting server displays your glucose and treatment data, and creates reports for detailed analysis. There are currently two reporting servers available for use with AAPS : [Nightscout](../SettingUpAaps/SettingUpTheReportingServer.md#nightscout) and [Tidepool](../SettingUpAaps/SettingUpTheReportingServer.md#tidepool). They both provide ways to visualize your diabetes data over time, provide statistics about the **time in range** (TIR) and other measures.

The Reporting server is independent of the other modules. If you don’t want to use a reporting server, you should know that it is not mandatory for running **AAPS** in the long term. But you still need to set up one as it will be required to fulfill [**Objective 1**](../SettingUpAaps/CompletingTheObjectives.md#objective-1-setting-up-visualization-and-monitoring-analyzing-basals-and-ratios).

Additional information on how to set up your reporting server can be found [here](../SettingUpAaps/SettingUpTheReportingServer.md).

## Дополнительные модули

### Смарт часы

You can choose any smartwatch with Android WearOS 1.x up to 4.x. **Beware, WearOS 5.x is not compatible!**

The Sony Smartwatch 3 (SWR50) is commonly used amongst loopers as it is the only watch that can get readings from Dexcom G6/G5 when phone is out of range. Некоторые другие часы могут быть модифицированы как самостоятельный коллектор (см. [эту документацию](https://github.com/NightscoutFoundation/xDrip/wiki/Patching-Android-Wear-devices-for-use-with-the-G5) для подробностей).

Пользователи создают список протестированных телефонов [и часов](https://docs.google.com/spreadsheets/d/1gZAsN6f0gv6tkgy9EBsYl0BQNhna0RDqA9QGycAqCQc/edit?usp=sharing). There are different watchfaces for use with **AAPS**, which you can find [here](../UsefulLinks/WearOsSmartwatch.md).

Для того, чтобы включить в список телефон, который не занесен в таблицу, заполните форму [](https://docs.google.com/forms/d/e/1FAIpQLScvmuqLTZ7MizuFBoTyVCZXuDb__jnQawEvMYtnnT9RGY6QUw/viewform).

Any problems with the spreadsheet please email [hardware@androidaps.org](mailto:hardware@androidaps.org), any donations of phone/watch models that still need testing please email [donations@androidaps.org](mailto:donations@androidaps.org).

### xDrip +

Even if you don't need to have the [xDrip+ App](https://xdrip.readthedocs.io/en/latest/) as **BG Source**, you can still use it for _i.e._ alarms or a different blood glucose display. You can have as many alarms as you want, specify the time when the alarm should be active, if it can override silent mode, etc. Some xDrip+ information can be found [here](../CompatibleCgms/xDrip.md). Имейте в виду, что документация к этому приложению не всегда актуальна, так как проект развивается довольно быстро.

## Что делать во время ожидания модулей

It sometimes takes a while to get all the modules for closing the loop. Но не беспокойтесь, можно многое сделать во время ожидания. It is **necessary** to check and (where appropriate) adapt basal rates (BR), insulin-carbratio (IC), insulin-sensitivity-factors (ISF) etc. And maybe open loop can be a good way to test the system and get familiar with **AAPS**. Using this mode, **AAPS** gives treatment recommendations you can manually execute.

Продолжайте читать документацию, общаться с другими пользователями в сети или вне ее, узнавать мнение пользователей (при этом учитывая, что подходят не все рекомендации).

**Done?** If you have your **AAPS** components all together (congrats!) or at least enough to start in open loop mode, you should first read through the [Objective description](../SettingUpAaps/CompletingTheObjectives.md) before each new Objective and setup up your hardware.