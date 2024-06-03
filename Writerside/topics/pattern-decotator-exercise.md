# Задача

## Условие

Вы создаете приложение для кафе, где клиенты могут заказывать кофе и добавлять в него различные добавки. Вы должны использовать паттерн "Декоратор" для реализации этой системы. Основной класс будет представлять базовый кофе, а декораторы будут добавлять к нему различные добавки, такие как молоко, шоколад, карамель и другие.

## Требования

1.	Создайте базовый класс `Coffee`, который будет иметь методы для получения описания и стоимости.
2. Создайте абстрактный класс `CoffeeDecorator`, который будет расширять класс `Coffee`.
3.	Реализуйте несколько конкретных декораторов, таких как `MilkDecorator`, `ChocolateDecorator` и `CaramelDecorator`, которые будут добавлять функциональность и изменять стоимость базового кофе.

## Пример

```python
# Базовый класс
class Coffee:
    def get_cost(self):
        return 5
    
    def get_description(self):
        return "Basic Coffee"
        
# ... ваш код

basic_coffee = Coffee()
print(basic_coffee.get_description())
print(basic_coffee.get_cost())

milk_coffee = MilkDecorator(basic_coffee)
print(milk_coffee.get_description())
print(milk_coffee.get_cost())

chocolate_milk_coffee = ChocolateDecorator(milk_coffee)
print(chocolate_milk_coffee.get_description())
print(chocolate_milk_coffee.get_cost())

caramel_chocolate_milk_coffee = CaramelDecorator(
    chocolate_milk_coffee)
print(caramel_chocolate_milk_coffee.get_description())
print(caramel_chocolate_milk_coffee.get_cost())
```

### Вывод

```bash
Basic Coffee
5
Basic Coffee, Milk
6
Basic Coffee, Milk, Chocolate
8
Basic Coffee, Milk, Chocolate, Caramel
11
```
