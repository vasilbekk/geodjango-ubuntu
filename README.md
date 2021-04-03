# Кто такой этот ваш «GeoDjango»?
Это библиотека для расщирения возможностей обычного Django, которая позволяет быстро и удобно работать с пространственными данными.

## Установка необходимых утилит

```
$ sudo apt-get install binutils libproj-dev gdal-bin
```

❗ При установке у вас может не оказаться какого-либо пакета и вас попросят его установить.

## GEOS
GEOS - это библиотека C ++ для выполнения геометрических операций и представление внутренней геометрии по умолчанию, используемое GeoDjango (за «ленивыми» геометриями). В частности, библиотека C API вызывается (например libgeos_c.so) непосредственно из Python с использованием ctypes.

📝 Можете заменить версию

```
$ wget https://download.osgeo.org/geos/geos-3.9.1.tar.bz2
$ tar xjf geos-3.9.1.tar.bz2
```
```
$ cd geos-3.9.1
$ ./configure
$ make
$ sudo make install
$ cd ..
```

## PROJ.4
PROJ.4 - это библиотека для преобразования геопространственных данных в различные системы координат.
Сначала загрузите исходный код PROJ.4 и файлы сдвига датума:

📝 Можете заменить версию

```
$ wget https://download.osgeo.org/proj/proj-7.2.1.tar.gz
$ wget https://download.osgeo.org/proj/proj-datumgrid-1.5.tar.gz
```
Затем распакуйте архив исходного кода и извлеките файлы сдвига датума в dataподкаталог (используйте nad подкаталог для PROJ <6.x). Это необходимо сделать перед настройкой:
```
$ tar xzf proj-7.2.1.tar.gz
$ cd proj-7.2.1/data
$ tar xzf ../../proj-datumgrid-1.5.tar.gz
$ cd ..
```
Теперь конфигурируем и устанавливаем:
```
$ ./configure
$ make
$ sudo make install
$ cd ..
```

## GDAL
GDAL - отличная геопространственная библиотека с открытым исходным кодом, которая поддерживает чтение большинства векторных и растровых форматов пространственных данных. В настоящее время, GeoDjango поддерживает только векторные данные библиотеки GDAL по возможности [2] . GEOS и PROJ.4 должны быть установлены до создания GDAL.

Давайте загрузим и распакуем:
```
$ wget https://download.osgeo.org/gdal/X.Y.Z/gdal-X.Y.Z.tar.gz
$ tar xzf gdal-X.Y.Z.tar.gz
$ cd gdal-X.Y.Z
```
Настроим, изготовим и установим:
```
$ ./configure
$ make # Go get some coffee, this takes a while.
$ sudo make install
$ cd ..
```



