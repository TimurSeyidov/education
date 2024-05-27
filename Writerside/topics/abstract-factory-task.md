# Задание

## Условние

Предположим, у вас есть фабрика по производству автомобилей. Автомобили могут быть различных типов: электрические, бензиновые и гибридные. Каждый тип автомобиля имеет свои уникальные характеристики, такие как мощность двигателя, расход топлива (или заряда), и т.д.

## Требования

1. Создайте абстрактную фабрику `CarFactory`, которая будет содержать методы для создания различных типов автомобилей: `ElectricCar`, `PetrolCar` и `HybridCar`.
2. Создайте три конкретные реализации абстрактной фабрики: `ElectricCarFactory`, `PetrolCarFactory` и `HybridCarFactory`.
3. Каждая из них должна реализовывать методы для создания соответствующих типов автомобилей.
4. Создайте абстрактный класс `Car`, который будет представлять собой общий интерфейс для всех типов автомобилей.
5. Реализуйте конкретные классы для каждого типа автомобилей: `ElectricCar`, `PetrolCar` и `HybridCar`.
6. Напишите код, который будет использовать абстрактную фабрику для создания экземпляров различных типов автомобилей.

## Пример использования

```python
electric_factory = ElectricCarFactory()
petrol_factory = PetrolCarFactory()
hybrid_factory = HybridCarFactory()

electric_car = electric_factory.produce_car()
petrol_car = petrol_factory.produce_car()
hybrid_car = hybrid_factory.produce_car()

electric_car.drive()
# Output: Driving an electric car.
petrol_car.drive()
# Output: Driving a petrol car.
hybrid_car.drive()
# Output: Driving a hybrid car.
```