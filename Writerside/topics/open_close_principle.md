#  Принцип открытости/закрытости

Принцип открытости/закрытости впервые был сформулирован Бернардом Мейером в 1988 году. Роберт К. Мартин говорил о нем так «Наиболее важный принцип открытости/закрытости гласит «Сущности программы (классы, модули, функции и т.п.) должны быть открыты для расширения, но закрыты для изменений».
Следование этому принципу гарантирует, что класс определен достаточно, чтобы делать то, что он должен делать. Добавление любых дополнительных функций может быть реализовано путем создания новых сущностей, которые расширяют возможности существующего класса и добавляют дополнительные функции самим себе. Таким образом можно предотвратить частые и тривиальные изменения в хорошо зарекомендовавшем себя классе низкого уровня.
Допустим, у нас есть приложение для магазина одежды. Среди функций системы есть функция применения специальных скидок в зависимости от типа одежды.
Пример ниже показывает один из способов реализации этого требования.
В примере у нас есть класс `DiscountCalculator`, который умеет хранить тип одежды. В нем есть функция, которая рассчитывает скидку в зависимости от типа одежды и возвращает новую стоимость за вычетом суммы скидки.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from enum import Enum

class Products(Enum):
    SHIRT = 1
    TSHIRT = 2
    PANT = 3


class DiscountCalculator():
    def __init__(self, product_type, cost):
        self.product_type = product_type
        self.cost = cost

    def get_discounted_price(self):
        if self.product_type == Products.SHIRT:
            return self.cost - (self.cost * 0.10)
        elif self.product_type == Products.TSHIRT:
            return self.cost - (self.cost * 0.15)
        elif self.product_type == Products.PANT:
            return self.cost - (self.cost * 0.25)


dc_shirt = DiscountCalculator(Products.SHIRT, 100)
print(dc_shirt.get_discounted_price())

dc_tshirt = DiscountCalculator(Products.TSHIRT, 100)
print(dc_tshirt.get_discounted_price())

dc_pant = DiscountCalculator(Products.PANT, 100)
print(dc_pant.get_discounted_price())

]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
enum Products
{
    case SHIRT;
    case TSHIRT;
    case PANT;
}

class DiscountCalculator {
    private Products $product_type;
    private float $cost = 0;

    public function __construct(Products $product_type, float $cost = 0) {
        $this->product_type = $product_type;
        $this->cost = $cost;
    }

    public function get_discounted_price() {
        if ($this->product_type === Products::SHIRT) {
            return $this->cost - ($this->cost * 0.10);
        }
        if ($this->product_type === Products::TSHIRT) {
            return $this->cost - ($this->cost * 0.15);
        }

        if ($this->product_type === Products::PANT) {
            return $this->cost - ($this->cost * 0.25);
        }
    }
}

$dc_shirt = new DiscountCalculator(Products::SHIRT, 100)
echo $dc_shirt->get_discounted_price() . PHP_EOL;

$dc_tshirt = new DiscountCalculator(Products::TSHIRT, 100)
echo $dc_tshirt->get_discounted_price() . PHP_EOL;

$dc_pant = new DiscountCalculator(Products::PANT, 100)
echo $dc_pant->get_discounted_price() . PHP_EOL;

]]>
</code-block>
</tab>
</tabs>


```bash
90.0
85.0
75.0
```

Эта конструкция нарушает принцип открытости/закрытости, поскольку этот класс потребует изменения, если будет добавляться какой-то тип одежды или если сумма скидки на какую-либо одежду изменится.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from enum import Enum
from abc import ABCMeta, abstractmethod

class DiscountCalculator():

    @abstractmethod
    def get_discounted_price(self):
        pass

class DiscountCalculatorShirt(DiscountCalculator):
    def __init__(self, cost):
        self.cost = cost

    def get_discounted_price(self):
        return self.cost - (self.cost * 0.10)

class DiscountCalculatorTshirt(DiscountCalculator):
    def __init__(self, cost):
        self.cost = cost

    def get_discounted_price(self):
        return self.cost - (self.cost * 0.15)

class DiscountCalculatorPant(DiscountCalculator):
    def __init__(self, cost):
        self.cost = cost

    def get_discounted_price(self):
        return self.cost - (self.cost * 0.25)


dc_shirt = DiscountCalculatorShirt(100)
print(dc_shirt.get_discounted_price())

dc_tshirt = DiscountCalculatorTshirt(100)
print(dc_tshirt.get_discounted_price())

dc_pant = DiscountCalculatorPant(100)
print(dc_pant.get_discounted_price())

]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
interface DiscountCalculator {
    public function get_discounted_price();
}

abstract class AbstractDiscountCalculator {
    protected float $cost = 0;

    public function __construct(float $cost = 0) {
        $this->cost = $cost;
    }
}

class DiscountCalculatorShirt extends AbstractDiscountCalculator implements DiscountCalculator {

    public function get_discounted_price() {
        return $this->cost * 0.9;
    }
}

class DiscountCalculatorTshirt extends AbstractDiscountCalculator implements DiscountCalculator {

    public function get_discounted_price() {
        return $this->cost * 0.85;
    }
}

class DiscountCalculatorPant extends AbstractDiscountCalculator implements DiscountCalculator {

    public function get_discounted_price() {
        return $this->cost * 0.75;
    }
}

$dc_shirt = new DiscountCalculatorShirt(100);
echo $dc_shirt->get_discounted_price() . PHP_EOL;

$dc_tshirt = new DiscountCalculatorTshirt(100);
echo $dc_tshirt->get_discounted_price() . PHP_EOL;

$dc_pant = new DiscountCalculatorPant(100);
echo $dc_pant->get_discounted_price() . PHP_EOL;

]]>
</code-block>
</tab>
</tabs>

```bash
90.0
85.0
75.0
```

Как видно из примера выше, теперь у нас есть очень простой базовый класс `DiscountCalculator` с одним абстрактным методом `get_discounted_price`. Мы создали новые классы для одежды, которые расширяют базовый класс `DiscountCalculator`. Следовательно, теперь каждый подкласс будет реализовывать функционал скидок самостоятельно. Сделав так, мы устранили предыдущие ограничения, которые требовали внесения изменений в базовый класс. Теперь, не изменяя базовый класс, мы можем добавлять больше одежды, а также изменять размер скидки на отдельный вид одежды по мере необходимости.