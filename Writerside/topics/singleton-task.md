# Задание

## Условие

Давайте представим, что у вас есть игра, и вы хотите иметь только один экземпляр класса, отвечающего за управление настройками игры.

## Пример использования

```python
settings1 = GameSettings.get_instance()
settings2 = GameSettings.get_instance()

print(settings1 is settings2)

settings1.volume = 70
settings1.difficulty = "Hard"

print(settings2.volume)
print(settings2.difficulty)
```

## Вывод

```bash
True
70
Hard
```