# Подключение «GeoDjango» к Django-проекту.
GeoDjango — это библиотека для расширения возможностей обычного Django, которая позволяет быстро и удобно работать с пространственными данными.

## Установка необходимых утилит

```
$ sudo apt-get install binutils libproj-dev gdal-bin g++ pkg-config sqlite3 libtiff-dev
```

❗ При установке у вас может не оказаться какого-либо пакета и вас попросят его установить.

### GEOS
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

### PROJ.4
PROJ.4 - это библиотека для преобразования геопространственных данных в различные системы координат.
Сначала загрузите исходный код PROJ.4 и файлы сдвига датума:

📝 Можете заменить версию

#### Если у вас Debian/Ubuntu:

```
sudo apt-get install proj-bin
```

#### Иначе:

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

### GDAL
GDAL - отличная геопространственная библиотека с открытым исходным кодом, которая поддерживает чтение большинства векторных и растровых форматов пространственных данных. В настоящее время, GeoDjango поддерживает только векторные данные библиотеки GDAL по возможности [2] . GEOS и PROJ.4 должны быть установлены до создания GDAL.

📝 Можете заменить версию (сейчас 3.3.0)


Давайте загрузим и распакуем:

```
$ wget https://download.osgeo.org/gdal/X.Y.Z/gdal-X.Y.Z.tar.gz
$ tar xzf gdal-X.Y.Z.tar.gz
$ cd gdal-X.Y.Z
```
Настроим, изготовим и установим.

⏳ У меня заняло 33 минуты, так что приготовьте себе хороший кофе :)
```
$ ./configure
$ make 
$ sudo make install
$ cd ..
```

## Установка расширения в базе данных PostgreSQL
Устанавливаем `postgis`:
```
$ sudo apt-get install postgis
```

Подключаемся к нашей базе данных
```
$ sudo -u postgres psql postgres
```

Устанавливаем расширение
```
postgres=# CREATE EXTENSION postgis;
CREATE EXTENSION
```
Проверяем работоспособность:
```
postgres=# SELECT PostGIS_version();
            postgis_version            
---------------------------------------
 2.5 USE_GEOS=1 USE_PROJ=1 USE_STATS=1
(1 row)
```

## Настройка Django-проекта
Отредактируем настройки базы данных и добавим в приложения `django.contrib.gis'
```
INSTALLED_APPS = [
    ...
    'django.contrib.gis',
    ...
]
...
DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.postgis',
        ...
    }
}
```





