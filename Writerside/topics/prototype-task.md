# Задание

## Условие

В вашей компании разрабатывается система управления заказами. Вам нужно создать прототип объекта "Заказ", который будет содержать базовую информацию о заказе: номер заказа, список товаров и общую сумму заказа. Ваша задача - использовать паттерн Прототип для создания новых заказов на основе этого прототипа, изменяя только необходимые детали.

## Пример использование

```python
prototype_order = OrderPrototype()
prototype_order.order_number = 1001
prototype_order.products = ["Product A", "Product B", "Product C"]
prototype_order.total_price = 150.00

# Создаем новый заказ на основе прототипа
order1 = Order(prototype_order.clone())
order1.order_number = 1002  # Изменяем номер заказа
order1.total_price = 200.00  # Изменяем общую сумму заказа

# Создаем еще один новый заказ на основе прототипа
order2 = Order(prototype_order.clone())
order2.order_number = 1003  # Изменяем номер заказа
order2.products.append("Product D")  # Добавляем новый товар

# Выводим информацию о заказах
print("Order 1:")
print("Order Number:", order1.order_number)
print("Products:", order1.products)
print("Total Price:", order1.total_price)

print("\nOrder 2:")
print("Order Number:", order2.order_number)
print("Products:", order2.products)
print("Total Price:", order2.total_price)
```