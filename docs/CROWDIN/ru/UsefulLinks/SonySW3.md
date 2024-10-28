# Установка службы Google Play вручную для Sony Smartwatch 3

Sony Smartwach 3-одни из самых популярных часов дляс AAPS. К сожалению, осенью 2020 года Google прекратил поддержку устройств с операционной системой OS 1.5. Это приводит к проблемам при использовании Sony SW3 с AAPS 2.7 и выше.

Следующий обходной путь должен продлить время использования Sony Smartwatch 3, но имейте в виду, что необходимость перехода на новые часы рано или поздно наступит.

## 1. Скачайте свежую версию GService для Wear OS

- На сайте [apkmirror](https://www.apkmirror.com/apk/google-inc/google-play-services-android-wear/)можно найти новую версию приложения "Google Play Services (Wear OS)".

  Архитектура: armeabi-v7a, Минимальная версия: Android 6.0+, Screen DPI: nodpi

- Убедитесь в следующем:

  - Это новейшая версия?
  - Совместима ли она с Android 6.0+ (так как это версия Android wear, 7.0+ и выше не будет работать)?

- Рано или поздно, Google определённо прекратит поддержку Android 6.0. Когда это произойдет, последняя версия больше не будет доступна для Android 6.0+.

## 2. Скачайте/установить инструменты adb на вашем компьютере

- Есть несколько способов установки утилиты отладки adb.
- Рекомендуется использовать [SDK Platform Tools ](https://developer.android.com/studio/releases/platform-tools): Просто скачайте zip-файл и распакуйте архив в выбранную директорию.

## 3. Включите параметры отладки ADB на ваших часах

- Включите режим разработчика, перейдя в Настройки --> About --> Номер сборки
- Или может быть Настройки --> Система --> О -->  --> Версии --> Build number

- Щелкните по нему 7 раз.
- Теперь перейдите в Настройки --> Параметры разработчика --> Отладка ADB (включено)

## 4. Подключите ваши часы к компьютеру

- Затем подключите часы к ПК.
- Переименуйте последние загруженные Google Play Service APK используя какое-нибудь короткое и простое имя (скажем SW3fix.apk).
- Поместите этот APK в директорию adb (в нашем случае: каталог разархивированных SDK Platform Tools).
- Откройте терминал Windows с помощью команды «cmd» в меню запуска Windows.
- В терминале, перейдите в каталог, который включает инструмент adb и Google Services APK (введите команду „cd C:UsersSWR50loopersdktools“).
- * Затем введите "adb devices".
- Через несколько секунд вы получите запрос на разрешение отладки на часах: примите его.
- *Когда вы снова напечатаете в терминале"adb devices", там появится что-то вроде "14452D11F536B52 device".
- Если вы видите "unauthorized" или что-то вроде того, то вы не готовы к следующему шагу, вернитесь назад и повторите попытку.
- Если этот шаг не получается, вам могут понадобиться недостающие драйверы для часов. Google вам поможет их отыскать.
- Затем подождите, установка может занять несколько минут.

## 5. Отправьте приложение на часы

- In terminal enter this command „adb install -r -g aplicationname.apk“ (so in our case „adb install -r -g SW3fix.apk“).

  ![Terminal command](../images/SonySW3_Terminal1.png)

- Дождитесь завершения установки примерно 4–5 минут.

  ![Terminal successful installation](../images/SonySW3_Terminal2.png)

- После завершения перезагрузите часы, и вы увидите синхронизацию приложений.