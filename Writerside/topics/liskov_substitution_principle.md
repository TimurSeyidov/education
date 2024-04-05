# Принцип подстановки Барбары Лисков

Принцип подстановки Лисков для многих - один из самых сложных принципов.
Принцип подстановки Лисков гласит: «Объекты в программе должны быть заменяемы экземплярами их подтипов без ущерба корректности работы программы».
Принцип подстановки Лисков был предложен Барбарой Лисков. Он предполагает отношение подтипов, называемое сильным поведенческим подтипом. Этот принцип говорит нам о том, что если класс `Sub` является подтипом класса `Sup`, тогда в программе объекты типа `Sup` должны легко заменяться объектами типа `Sub` без необходимости изменения кода. Дядя Боб включил этот принцип в число 5 лучших принципов проектирования SOLID.
Допустим, у нас есть базовый класс `Car`, который отвечает за тип автомобиля. Класс `Car` наследуется подклассом `PetrolCar`. Аналогично, базовый класс `Car` может быть унаследован другими классами, которые могут расширять его возможности.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
class Car():
    def __init__(self, type):
        self.type = type

class PetrolCar(Car):
    def __init__(self, type):
        self.type = type


car = Car("SUV")
car.properties = {"Color": "Red", "Gear": "Auto", "Capacity": 6}

petrol_car = PetrolCar("Sedan")
petrol_car.properties = ("Blue", "Manual", 4)

cars = [car, petrol_car]

def find_red_cars(cars):
red_cars = 0
for car in cars:
    if car.properties['Color'] == "Red":
        red_cars += 1
print(f'Number of Red Cars = {red_cars}')

find_red_cars(cars)
]]>
</code-block>
<br/>
<code-block lang="bash">
<![CDATA[
Traceback (most recent call last):
  File "main.py", line 25, in <module>
    find_red_cars(cars)
  File "main.py", line 21, in find_red_cars
    if car.properties['Color'] == "Red":
TypeError: tuple indices must be integers or slices, not str


** Process exited - Return Code: 1 **
Press Enter to exit terminal
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
class Car {
    public array $properties = [];
    public string $type;

    public function __construct(string $type) {
        $this->type = $type;
    }
}

class PetrolCar extends Car {}

$car = new Car("SUV");
$car->properties = [
    "Color" => "Red",
    "Gear" => "Auto",
    "Capacity" => 6
];

$petrol_car = new PetrolCar("Sedan");
$petrol_car->properties = ["Blue", "Manual", 4];

$cars = [$car, $petrol_car];

function find_red_cars($cars) {
    $red_cars = 0;
    foreach ($cars as $car) {
        if ($car->properties['Color'] === "Red") {
            $red_cars += 1;
        }
    }
    echo 'Number of Red Cars = ' . $red_cars;
}

find_red_cars($cars);
]]>
</code-block>
<br/>
<code-block lang="bash">
<![CDATA[
Warning: Undefined array key "Color" in /home/user/scripts/code.php on line 29
Number of Red Cars = 1
]]>
</code-block>
</tab>
</tabs>

Как видно из кода, мы пытаемся просмотреть список объектов `Car`. Именно здесь мы нарушаем принцип подстановки Лисков, поскольку мы не можем заменить объекты супертипа `Car` объектами подтипа `PetrolCar` внутри функции поиска красных автомобилей.
Лучшим вариантом было бы реализовать методы **setter** и **getter** в суперклассе `Car`. С их помощью мы можем устанавливать и получать свойства автомобиля, не оставляя эту реализацию последующим разработчикам. Таким образом, мы просто получаем свойства с помощью метода `setter`, и его реализация остается инкапсулированной в суперклассе.
Так мы сможем соблюсти принцип подстановки Лисков, как показано ниже:

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
class Car():
    def __init__(self, type):
        self.type = type
        self.car_properties = {}

    def set_properties(self, color, gear, capacity):
        self.car_properties = {"Color": color, "Gear": gear, "Capacity": capacity}

    def get_properties(self):
        return self.car_properties

class PetrolCar(Car):
    def __init__(self, type):
        self.type = type
        self.car_properties = {}


car = Car("SUV")
car.set_properties("Red", "Auto", 6)

petrol_car = PetrolCar("Sedan")
petrol_car.set_properties("Blue", "Manual", 4)

cars = [car, petrol_car]

def find_red_cars(cars):
    red_cars = 0
    for car in cars:
        if car.get_properties()['Color'] == "Red":
            red_cars += 1
    print(f'Number of Red Cars = {red_cars}')

find_red_cars(cars)
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
class Car {
    protected array $properties = [];
    public string $type;

    public function __construct(string $type) {
        $this->type = $type;
    }

    public function set_properties(string $color, string $gear, int $capacity) {
        $this->properties['Color'] = $color;
        $this->properties['Gear'] = $gear;
        $this->properties['Capacity'] = $capacity;
    }

    public function get_properties() {
        return $this->properties;
    }
}

class PetrolCar extends Car {}

$car = new Car("SUV");
$car->set_properties("Red", "Auto", 6);

$petrol_car = new PetrolCar("Sedan");
$petrol_car->set_properties("Blue", "Manual", 4);

$cars = [$car, $petrol_car];

function find_red_cars($cars) {
    $red_cars = 0;
    foreach ($cars as $car) {
        if ($car->get_properties()['Color'] === "Red") {
            $red_cars += 1;
        }
    }
    echo 'Number of Red Cars = ' . $red_cars;
}

find_red_cars($cars);
]]>
</code-block>
</tab>
</tabs>
```bash
Number of Red Cars = 1
```