# Задание

## Условие

Вам нужно создать систему для управления различными типами источников данных. У вас есть две разные системы для чтения данных: одна из текстовых файлов и другая из базы данных. Требуется объединить их в едином интерфейсе для удобного использования.

1. Создайте интерфейс `DataSource`, который будет иметь метод `read_data()`.
2. Создайте класс `FileDataSource`, который реализует интерфейс `DataSource` и читает данные из текстового файла.
3. Создайте класс `DatabaseDataSource`, который реализует интерфейс `DataSource` и читает данные из базы данных.
4. Создайте адаптер `DatabaseAdapter`, который позволит классу `DatabaseDataSource` работать через интерфейс `DataSource`.

## Требования

1. Класс `FileDataSource` должен принимать в конструкторе путь к файлу и реализовать метод `read_data()`, который возвращает содержимое файла.
2. Класс `DatabaseDataSource` должен имитировать чтение данных из базы данных. В конструкторе он должен принимать строку подключения, а метод `fetch_data()` должен возвращать данные.
3. Адаптер `DatabaseAdapter` должен принимать объект `DatabaseDataSource` в конструкторе и реализовать метод `read_data()`, вызывая метод `fetch_data()` у `DatabaseDataSource`.

## Пример использования

```python
file_source = FileDataSource("data.txt")
print(file_source.read_data())

database_source = DatabaseDataSource("database_connection_string")
database_adapter = DatabaseAdapter(database_source)
print(database_adapter.read_data())
```
