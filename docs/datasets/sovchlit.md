# Советские христоматии (литература)

!!! info ""
    **ruts.datasets.SovChLit**

## Описание

Модуль для работы с набором данных советских хрестоматий по литературе.

Для формирования набора данных используются оцифрованные издания проекта ["Школьные учебники СССР"](https://sheba.spb.ru/shkola/):

*   Родная речь. Книга для чтения в I классе начальной школы. Е.Е. Соловьева, Л.А. Карпинская, Н.Н. Щепетова

## Параметры

| Параметр | Тип | По умолчанию | Описание |
| :------: | :-: | :----------: | :------: |
| `data_dir` | str | `DEFAULT_DATA_DIR.joinpath("texts")` | Путь к директории с набором данных |

## Атрибуты

| Атрибут | Тип | Описание |
| :-----: | :-: | :------: |
| `labels` | tuple[str] | Кортеж уровней сложности текстов |

## Методы

### download

Выполняет загрузку набора данных из сети и извлечение файлов.

Параметры:

| Параметр | Тип | По умолчанию | Описание |
| :------: | :-: | :----------: | :------: |
| `force` | bool | `-` | Загрузить набор данных, даже если он уже загружен |

Рассмотрим пример загрузки набора данных и вывод информации о нем:

!!! example "Пример"

    _Код_:

    ``` python
    # Загрузка библиотек
    from ruts.datasets import SovChLit

    # Создание объекта набора данных
    sc = SovChLit(data_dir='.')

    # Загрузка набора данных
    sc.download(force=True)

    # Отображение информации о наборе данных
    sc.info
    ```

    _Результат_:

    ``` bash
    {'description': 'Корпус советских хрестоматий по литературе',
    'url': 'https://dataverse.harvard.edu/file.xhtml?fileId=3670902&version=DRAFT',
    'Наименование': 'sov_chrest_lit'}
    ```

### get_texts

Выполняет извлечение текстов (без заголовков) из набора данных.

Параметры:

| Параметр | Тип | По умолчанию | Описание |
| :------: | :-: | :----------: | :------: |
| `grade` | int | `-` | Уровень сложности текстов |
| `book` | str | `-` | Наименование книги |
| `year` | int | `-` | Год издания книги |
| `category` | str | `-` | Категория текстов |
| `text_type` | str | `-` | Тип текстов |
| `subject` | str | `-` | Наименование текстов |
| `author` | str | `-` | Автор текстов|
| `min_len` | int | `-` | Минимальная длина текста (в символах) |
| `max_len` | int | `-` | Максимальная длина текста (в символах) |
| `limit` | int | `-` | Количество текстов |

Рассмотрим пример извлечения текстов из набора данных, выбрав только 1 текст из категории "Весна" длиной не более 100 символов:

!!! example "Пример"

    _Код_:

    ``` python
    # Загрузка библиотек
    from ruts.datasets import SovChLit

    # Создание объекта набора данных
    sc = SovChLit()

    # Отображение извлеченных текстов
    for i in sc.get_texts(max_len=100, category='Весна', limit=1):
        print(i)
    ```

    _Результат_:

    ``` bash
    В марте курочка под порожком водицы напьётся.
    Март с водой, апрель с травой.
    В апреле земля преет.
    ```

### get_records

Выполняет извлечение записей (с заголовками) из набора данных.

Параметры:

| Параметр | Тип | По умолчанию | Описание |
| :------: | :-: | :----------: | :------: |
| `grade` | int | `-` | Уровень сложности текстов |
| `book` | str | `-` | Наименование книги |
| `year` | int | `-` | Год издания книги |
| `category` | str | `-` | Категория текстов |
| `text_type` | str | `-` | Тип текстов |
| `subject` | str | `-` | Наименование текстов |
| `author` | str | `-` | Автор текстов|
| `min_len` | int | `-` | Минимальная длина текста (в символах) |
| `max_len` | int | `-` | Максимальная длина текста (в символах) |
| `limit` | int | `-` | Количество текстов |

Рассмотрим пример извлечения записей из набора данных, выбрав только 1 запись из категории "Весна" длиной не более 100 символов:

!!! example "Пример"

    _Код_:

    ``` python
    # Загрузка библиотек
    from ruts.datasets import SovChLit

    # Создание объекта набора данных
    sc = SovChLit()

    # Отображение извлеченных текстов
    for i in sc.get_records(max_len=100, category='Весна', limit=1):
        print(i)
    ```

    _Результат_:

    ``` bash
    {'author': 'Е. Трутнева',
    'book': 'Родная речь. Книга для чтения в I классе начальной школы',
    'category': 'Весна',
    'file': PosixPath('../ruTS/ruts_data/texts/sov_chrest_lit/grade_1/155'),
    'grade': 1,
    'subject': 'Дождик',
    'text': 'В марте курочка под порожком водицы напьётся.\n'
            'В марте курочка под порожком водицы напьётся.\n'
            'В апреле земля преет.',
    'type': 'Стихотворение',
    'year': 1963}
    ```