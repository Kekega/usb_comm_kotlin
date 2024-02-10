# USB-Communicator-App
## Что это такое
Данное приложение позволяет коммуницировать с ПК на Linux, MacOS или Windows (двустороняя коммуникация).
Коммуникация с ПК происходит с помощью Android Accessory Protocol, в данном случае [Python-скрипт](https://github.com/alien-agent/USB-Communicator-Script) на ПК презентует себя как акссессуар.

Поиск доступного устройства происходит полностью автоматически, никаких дополнительных действий для переключения между режимами Arduino/PC выполнять не нужно.

## Подключение к ПК
1. Подключить смартфон с установленным приложением к ПК с помощью кабеля. 
**В случае Windows необходимо установить правильные драйвера**, чтобы смартфон определялся как USB-устройство, а не MTP. На MacOS и Linux дополнительных действий не требуется.
2. Запустить скрипт в соответствии с инструкцией в режиме read или write.
3. Дождаться, пока скрипт переведет смартфон в Accessory Mode.
4. Должен сработать USB-Filter, который автоматически предложит открыть данное приложение. Также его можно открыть вручную.
5. Приложение запросит разрешение на доступ к USB-устройству. Если приложение было открыто через IntentFilter, доступ будет выдан автоматически.
В случае успеха, в приложении будет отображаться заголовок `Connected to Accessory`.
6. Готово!

Запуск приложения и скрипта, а также подключение кабеля можно осуществлять в любом порядке, приложение самостоятельно увидит, что ПК появился в списке доступных устройств и запросит доступ.

## Возможные проблемы
Python-скрипт может выдавать ошибку `no backend available`. Это означает что в системе не установлена `libusb`, либо установлены неправильные драйвера для смартфона (в случае Windows).
Также эта ошибка возможна в случае если библиотеке pyusb не удалось найти путь к `libusb`. В таком случае его нужно указать вручную, см. пример в начале файла для MacOS с процессором Apple Silicon.

Вылетает на шаге `Triggering accessory mode` - нет правильных драйверов (Windows). Телефон не должен определяться как MTP/FTP/...
Берем программу https://zadig.akeo.ie и прошиваем на телефон драйвер libusb (libusb предварительно нужно установить).