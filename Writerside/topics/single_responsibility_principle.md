# Принцип единственной ответственности

Принцип единой ответственности гласит, что у каждого класса должна быть только одна «ответственность» и он не должен брать на себя другие обязанности. Роберт К. Мартин объяснял его так: «У класса должна быть лишь одна причина для изменения».
Давайте в качестве примера возьмем приложение телефонного справочника. Мы будем делать телефонный справочник, в котором будет класс `TelephoneDirectory`. Он будет «нести ответственность» за ведение записей справочника, то есть телефонных номеров и названий организаций, которым принадлежат номера. Ожидается, что класс будет выполнять следующие операции:
- добавлять новую запись (`Name` и `Telephone Number`)
- удалять существующую запись
- изменять номер телефона, присвоенный сущности `Name`
- предоставлять поиск, который будет возвращать номер, присвоенный сущности `Name`.

Класс `TelephoneDirectory` может выглядеть следующим образом:

```python
class TelephoneDirectory:
    def __init__(self):
        self.telephone_directory = dict()
        
    def add_entry(self, name, number):
        self.telephone_directory[name] = number
        
    def delete_entry(self, name):
        del self.telephone_directory[name]
    
    def update_entry(self, name, number):
        self.telephone_directory[name] = number
        
    def lookup_number(self, name):
        return self.telephone_directory.get(name)
        
    def __str__(self):
        ret_dct = ''
        for key, value in self.telephone_directory.items():
            ret_dct += f'{key} : {value}\n'
        return ret_dct

phone_book = TelephoneDirectory()
phone_book.add_entry('Ravi', 123456)
phone_book.add_entry('Vikas', 67890)
print(phone_book)

phone_book.delete_entry('Ravi')
phone_book.add_entry('Ravi', 123456)
phone_book.update_entry('Vikas', 776589)
print(phone_book.lookup_number('Vikas'))
print(phone_book)
```

```bash
Ravi : 123456
Vikas : 67890

776589
Vikas : 776589
Ravi : 123456
```

Сейчас наш класс `TelephoneDirectory` выглядит хорошо, в нем точно реализованы ожидаемые функции:
А теперь скажем, что в проекте есть еще два требования – Сохранить содержимое справочника в базе данных и перенести содержимое справочника в файл.
Теперь добавим еще два метода в класс `TelephoneDirectory`, как показано ниже:

```python
class TelephoneDirectory:
    def __init__(self):
        self.telephone_directory = dict()
        
    def add_entry(self, name, number):
        self.telephone_directory[name] = number
        
    def delete_entry(self, name):
        del self.telephone_directory[name]
    
    def update_entry(self, name, number):
        self.telephone_directory[name] = number
        
    def lookup_number(self, name):
        return self.telephone_directory.get(name)
        
    def save_to_file(self, file_name, location):
        #код для сохранения телефонного справочника в файл
        pass
        
    def persist_to_database(self, database_details):
        #код для сохранения телефонного справочника в базу данных
        pass
        
    def __str__(self):
        ret_dct = ''
        for key, value in self.telephone_directory.items():
            ret_dct += f'{key} : {value}\n'
        return ret_dct
```

Так вот, именно сейчас мы нарушили принцип единственной ответственности. Добавив функции сохранения в базу данных и сохранения в файл, мы дали классу дополнительные обязанности, которые не входят в его основную зону ответственности. Теперь в классе есть дополнительные функции, которые могут привести к его изменению. В будущем, если появятся какие-то требования, связанные с сохранением данных, это может привести к изменениям в классе `TelephoneDirectory`. Получается, что класс `TelephoneDirectory` подвержен изменениям по причинам, которые не являются его основной ответственностью.
Принцип единственной ответственности требует от нас не добавлять дополнительные обязанности к классу, чтобы нам не приходилось менять класс, когда нам нужно изменить функционал сохранения справочника в базу данных или в файл. Мы можем передать экземпляр класса `TelephoneDirectory` экземплярам этих классов и записать любые дополнительные функции в них.
Так мы гарантируем, что у класса `TelephoneDirectory` есть лишь одна причина для изменения – это изменения в его основной «ответственности».

```python
class PersistToDatabase:
    def __init__(self, object_to_persist):
        pass
        
class SaveToFile:
    def __init__(self, object_to_save):
        pass
```