# Начало работы с PlatformIO в Atom под Linux

_В этой статье рассматривается как начать использовать [PlatformIO][] с [Atom][]
для разработки скетчей для [Arduino][] в среде Linux._

## Предварительная подготовка

До установки _PlatformIO_ в Linux нужно установить Python 2.7, Clang и Atom.
В Ubuntu для этого выполняем команды:

``` bash
sudo apt install python clang
```

Затем загружаем пакет Atom и устанавливаем:

``` bash
sudo dpkg -i atom-amd64.deb
```

Далее, нужно выяснить, какой файл устройства отвечает за подключённый Arduino,
скорее всего это будет `/dev/ttyACM0`. Для работы с ним нужно назначить 
соответствующие права. Для этого можно, например, добавить пользователя в
группу-владельца файла. В Ubuntu это делается так:

``` bash
sudo usermod -a -G dialout username
```

Для большего удобства работы с файлами устройств, представляющих подключённые 
устройства Arduino, нужно скачать и установить настройки для udev:

``` bash
wget https://raw.githubusercontent.com/platformio/platformio/develop/scripts/99-platformio-udev.rules
sudo cp 99-platformio-udev.rules /etc/udev/rules.d/
sudo service udev restart
```

Теперь, после подключения устройства Arduino, можно увидеть следующее:

```
Bus 002 Device 004: ID 2341:0043 Arduino SA Uno R3 (CDC ACM)
```

## Установка PlatformIO

PlatformIO можно установить в качестве инструмента командной строки, но в этой
статье рассматривается работа с ним в среде Atom.

После установки и запуска Atom нужно открыть менеджер пакетов Atom:
`Edit -> Preferences`, затем `Install`. В окне поиска набираем `platformio`
и выбираем для установки пакет _PlatformIO IDE_. После установки нужно перезапустить
Atom, после чего установка PlatformIO IDE продолжится.

## Работаем с проектом 

После установки PlatformIO IDE в Atom добавятся соответствующие меню, 
стартовое окно и панель инструментов.

Для создания проектов выбираем `New Project` в окне PlatformIO IDE или 
`PlatformIO -> Initialize new PlatformIO Project...` В появившемся диалоговом 
окне нужно выбрать аппаратную платформу и папку для размещения проекта.

Теперь, когда проект создан, можно добавить в него скетч. Для этого добавляем в
каталог `src` проекта модуль `main.cpp` и пишем в нём свою программу, например,
классическую мигалку:

``` c++
#include <Arduino.h>

void  setup() {
  Serial.begin(9600);
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  Serial.println("HIGH");
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  Serial.println("LOW");
  delay(1000);
}
``` 

Для сборки проекта используем команду `PlatformIO -> Build`, для выгрузки в 
Arduino `PlatformIO -> Upload`.

В итоге должны увидеть такую картину:

![Проект в PlatformIO IDE](/blog/platformio-getting-started-in-atom-under-linux/platformio-getting-started-in-atom-under-linux.png)

## Ссылки

[PlatformIO]: http://platformio.org/
[Atom]: https://atom.io/
[Arduino]: http://www.arduino.org/

* [PlatformIO][]
* [Atom][]
* [Arduino][]

## История изменений

_2016-06-14_ Добавлена информация по настройке udev.
