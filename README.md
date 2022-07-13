# Установка DVC

DVC можно установить несколькими способами? Которые указаны на [официальном сайте](https://dvc.org/doc/install).
В данном руководстве мы рассмотрим случай установки с использованием `pip`.

При использовании `pip` или `conda` необходимо установить пакеты с поддержкой `s3` удаленных хранилищ:
```bash
pip install "dvc[s3]" # Для pip
conda install -c conda-forge dvc-s3 # Для conda
```

DVC можно устанавливать как в систему, так и в виртуальную среду python.

# Создание нового проекта

## Инициализация

DVC сам по себе не занимается версионированием данных, вместо этого он использует git.

Поэтому порвым делом в корневой дирректории проекта необходимо инициализировать новый git репозиторий

```bash
git init
```

, или склонировать существующий без DVC

```bash
git clone [url удаленного репозитория]
```

После этого инициализируем DVC:

```bash
dvc init
```

Далее настроим удаленное хранилище для DVC

```bash
# Добавляем новое удаленное хранилище
dvc remote add spbstu-applied-math-yandex s3://202207dvc/projects/[имя_вашего_репозитория]

# Указываем адрес серверов
dvc remote modify spbstu-applied-math-yandex endpointurl https://storage.yandexcloud.net

# Сделаем хранилищем поумолчанию
dvc remote default spbstu-applied-math-yandex
```

Осталось [добавить ключ доступа](#добавление-ключа-доступа).

# Добавление ключа доступа

Для доступа к хранилищу вам необходимо получить ключ доступа на кафедре:

```bash
dvc remote modify --local spbstu-applied-math-yandex access_key_id "[идентификатор_ключа]"
dvc remote modify --local spbstu-applied-math-yandex secret_access_key "[секретный_ключ]"
```

Обязательно установите параметр `--local`, так как иначе ключ может попасть в общий конфиг и будет загружен на GitHub.

Имя хранилища может быть не `spbstu-applied-math-yandex`. В этом случае его можно найти командой `dvc remote list`, его адрес должен начинатся с `"s3://202207dvc/projects/"`

#

После этого можно начинать работу с системой контроля данных.
Краткие туториалы можно найти [здесь](https://dvc.org/doc/start), а справку по командам [тут](https://dvc.org/doc/command-reference).

Краткие сведения о базовых командах будут [перведены далее](#базовые-команды).

# Клонирование существующего проекта

Если вы склонировали проект, который уже добавлен в систему, то вам остается лишь [добавить ключ доступа](#добавление-ключа-доступа) сделать pull

```bash
dvc pull
```

# Базовые команды

## <В работе>