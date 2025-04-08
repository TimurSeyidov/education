# Задача

## Условие
Вы разрабатываете систему управления умным домом. Система состоит из нескольких подсистем:
- Система освещения
- Система климат-контроля
- Система безопасности
- Мультимедийная система

Каждая подсистема имеет свой собственный API с множеством методов и параметров. Ваша задача — создать фасад, который упростит взаимодействие с этими подсистемами и предоставит пользователю понятный и простой интерфейс для управления умным домом.


## Требования

1. Реализуйте классы для каждой подсистемы с соответствующими методами
2. Создайте класс Фасад, который инкапсулирует сложность работы с подсистемами
3. Реализуйте удобные методы в фасаде для типичных сценариев использования:
   - Режим "Я дома" (включает свет, устанавливает комфортную температуру, отключает сигнализацию)
   - Режим "Я ухожу" (выключает свет и технику, включает сигнализацию)
   - Режим "Вечеринка" (приглушенный свет, музыка, особый климат-режим)
   - Режим "Ночь" (выключает основное освещение, снижает температуру, включает сигнализацию)

## Пример

<tabs>
<tab title="Python">
    <code-block lang="python">
<![CDATA[
# Клиентский код
def main():
    print("=== Тестирование паттерна Фасад для умного дома ===")
    
    # Создаем экземпляр фасада
    smart_home = SmartHomeFacade()
    
    # Проверяем начальное состояние
    print("\n1. Начальное состояние всех систем:")
    print(smart_home.get_all_systems_status())
    
    # Проверяем режим "Я дома"
    print("\n2. Активация режима 'Я дома':")
    home_results = smart_home.home_mode()
    for result in home_results:
        print(f" - {result}")
    
    print("\n   Состояние систем после активации режима 'Я дома':")
    print(smart_home.get_all_systems_status())
    
    # Проверяем режим "Вечеринка"
    print("\n3. Активация режима 'Вечеринка':")
    party_results = smart_home.party_mode()
    for result in party_results:
        print(f" - {result}")
    
    print("\n   Состояние систем после активации режима 'Вечеринка':")
    print(smart_home.get_all_systems_status())
    
    # Проверяем режим "Ночь"
    print("\n4. Активация режима 'Ночь':")
    night_results = smart_home.night_mode()
    for result in night_results:
        print(f" - {result}")
    
    print("\n   Состояние систем после активации режима 'Ночь':")
    print(smart_home.get_all_systems_status())
    
    # Проверяем режим "Я ухожу"
    print("\n5. Активация режима 'Я ухожу':")
    away_results = smart_home.away_mode()
    for result in away_results:
        print(f" - {result}")
    
    print("\n   Состояние систем после активации режима 'Я ухожу':")
    print(smart_home.get_all_systems_status())
    
    print("\n=== Тестирование завершено ===")

if __name__ == "__main__":
    main()

]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
// Функция для красивого вывода массивов
function prettyPrint($array) {
    echo json_encode($array,
        JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
}

// Тестирование фасада
function testFacade() {
    echo "=== Тестирование паттерна Фасад для умного дома ===\n";
    
    // Создаем экземпляр фасада
    $smartHome = new SmartHomeFacade();
    
    // Проверяем начальное состояние
    echo "\n1. Начальное состояние всех систем:\n";
    prettyPrint($smartHome->getAllSystemsStatus());
    
    // Проверяем режим "Я дома"
    echo "\n\n2. Активация режима 'Я дома':\n";
    $homeResults = $smartHome->homeMode();
    foreach ($homeResults as $result) {
        echo " - $result\n";
    }
    
    echo "\n   Состояние систем после активации режима 'Я дома':\n";
    prettyPrint($smartHome->getAllSystemsStatus());
    
    // Проверяем режим "Вечеринка"
    echo "\n\n3. Активация режима 'Вечеринка':\n";
    $partyResults = $smartHome->partyMode();
    foreach ($partyResults as $result) {
        echo " - $result\n";
    }
    
    echo "\n   Состояние систем после активации режима 'Вечеринка':\n";
    prettyPrint($smartHome->getAllSystemsStatus());
    
    // Проверяем режим "Ночь"
    echo "\n\n4. Активация режима 'Ночь':\n";
    $nightResults = $smartHome->nightMode();
    foreach ($nightResults as $result) {
        echo " - $result\n";
    }
    
    echo "\n   Состояние систем после активации режима 'Ночь':\n";
    prettyPrint($smartHome->getAllSystemsStatus());
    
    // Проверяем режим "Я ухожу"
    echo "\n\n5. Активация режима 'Я ухожу':\n";
    $awayResults = $smartHome->awayMode();
    foreach ($awayResults as $result) {
        echo " - $result\n";
    }
    
    echo "\n   Состояние систем после активации режима 'Я ухожу':\n";
    prettyPrint($smartHome->getAllSystemsStatus());
    
    echo "\n\n=== Тестирование завершено ===\n";
}

// Запускаем тестирование
testFacade();

]]>
</code-block>
</tab>
</tabs>