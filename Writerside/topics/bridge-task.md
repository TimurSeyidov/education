# Задание

## Условие

Реализуйте систему для управления различными устройствами умного дома с использованием паттерна "Мост". У вас есть два типа устройств: телевизоры и лампочки. Каждое устройство может иметь несколько разных производителей, например, "Sony" и "Samsung" для телевизоров, "Philips" и "IKEA" для лампочек.

Необходимо создать абстракцию для устройств и конкретные реализации для каждого производителя. Также требуется создать интерфейс для управления этими устройствами, включающий методы включения, выключения и изменения состояния (например, смена канала для телевизора или изменение яркости для лампочки).

## Требования

1.  Создайте интерфейс `Device`, который определяет методы `turn_on()`, `turn_off()` и `set_state(state)`.
2. Реализуйте конкретные классы устройств: `TV` и `Light`, которые будут использовать интерфейс `Device`.
3. Создайте абстракцию `RemoteControl`, которая будет взаимодействовать с устройствами через интерфейс `Device`.
4. Реализуйте конкретные классы производителей, например, `SonyTV`, `SamsungTV`, `PhilipsLight`, `IKEALight`.
5. Создайте клиентский код, который демонстрирует использование созданной системы.

## Пример использования

```python
# Клиентский код
def main():
    sony_tv = SonyTV()
    samsung_tv = SamsungTV()
    philips_light = PhilipsLight()
    ikea_light = IKEALight()

    remote_for_sony = RemoteControl(sony_tv)
    remote_for_samsung = RemoteControl(samsung_tv)
    remote_for_philips = RemoteControl(philips_light)
    remote_for_ikea = RemoteControl(ikea_light)

    remote_for_sony.turn_on()
    remote_for_sony.set_state("HBO")
    remote_for_sony.turn_off()
    
    remote_for_samsung.turn_on()
    remote_for_samsung.set_state("CNN")
    remote_for_samsung.turn_off()

    remote_for_philips.turn_on()
    remote_for_philips.set_state("75%")
    remote_for_philips.turn_off()
    
    remote_for_ikea.turn_on()
    remote_for_ikea.set_state("50%")
    remote_for_ikea.turn_off()

if __name__ == "__main__":
    main()

```