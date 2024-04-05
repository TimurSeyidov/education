# Принцип разделения интерфейсов

Принцип разделения интерфейсов гласит что: «Ни один клиент не должен зависеть от методов, которые он не использует».
Принцип разделения интерфейсов был предложен Робертом К. Мартином, когда он консультировал компанию Xerox.
Принцип разделения интерфейсов предполагает создание небольших интерфейсов, известных как «ролевые интерфейсы», вместо большого интерфейса, состоящего из нескольких методов. Разделяя методы по ролям на более мелкие интерфейсы, клиенты будут зависеть только от методов, которые имеют к ним отношение.
Допустим, мы разрабатываем приложение для различных коммуникационных устройств. Мы говорим, что устройство связи – это устройство, которое будет иметь одну или несколько из следующих функций: совершать звонки, отправлять SMS или искать в Интернете. Итак, мы создаем интерфейс с именем `CommunicationDevice` и добавляем соответствующие абстрактные методы для каждой из этих функций, чтобы любой создаваемый класс смог реализовать эти методы.
Затем мы создаем класс `SmartPhone` с помощью интерфейса `CommunicationDevice` и реализуем функционал абстрактных методов. До сих пор все было в порядке.
Теперь предположим, что нам нужно создать стационарный телефон. Он тоже является устройством связи, поэтому мы создаем новый класс `LandlinePhone` через тот же интерфейс `CommunicationDevice`. Именно здесь мы сталкиваемся с проблемой из-за объемного интерфейса `CommunicationDevice`. В классе `LandlinePhone` мы реализовываем метод `make_calls()`, но поскольку мы также наследуем абстрактные методы `send_sms()` и `browse_internet()`, мы должны предоставить реализацию и этих двух абстрактных методов в классе `LandlinePhone`, даже если они в принципе неприменимы к этому виду телефонов. Мы можем либо создать исключение, либо оставить pass вместо реализации, но нам все равно нужно ее предоставить.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from abc import ABCMeta, abstractmethod

class CommunicationDevice():
    @abstractmethod
    def make_calls():
        pass

    @abstractmethod
    def send_sms():
        pass

    @abstractmethod
    def browse_internet():
        pass

class SmartPhone(CommunicationDevice):
    def make_calls():
        #implementation
        pass

    def send_sms():
        #implementation
        pass

    def browse_internet():
        #implementation
        pass

class LandlinePhone(CommunicationDevice):
    def make_calls():
        #implementation
        pass

    def send_sms():
        #just pass or raise exception as this feature is not supported 
        pass

    def browse_internet():
        #just pass or raise exception as this feature is not supported
        pass
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
interface CommunicationDevice {
    public function make_calls();
    public function send_sms();
    public function browse_internet();
}

class SmartPhone implements CommunicationDevice {
    public function make_calls() {
        // TO DO
    }

    public function send_sms() {
        // TO DO
    }

    public function browse_internet() {
        // TO DO
    }
}

class LandlinePhone implements CommunicationDevice {
    public function make_calls() {
        // TO DO
    }

    public function send_sms() {
        // just pass or raise exception as this feature is not supported
    }

    public function browse_internet() {
        // just pass or raise exception as this feature is not supported
    }
}

]]>
</code-block>
</tab>
</tabs>

Все можно исправить, следуя принципу разделения интерфейсов, как в примере ниже. Вместо создания большого интерфейса мы создаем более маленькие ролевые интерфейсы для каждого метода. Соответствующие классы будут использовать только связанные интерфейсы.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from abc import ABCMeta, abstractmethod

class CallingDevice():
    @abstractmethod
    def make_calls():
        pass

class MessagingDevice():
    @abstractmethod
    def send_sms():
        pass

class InternetbrowsingDevice():
    @abstractmethod
    def browse_internet():
        pass

class SmartPhone(CallingDevice, MessagingDevice, InternetbrowsingDevice):
    def make_calls():
        #implementation
        pass

    def send_sms():
        #implementation
        pass

    def browse_internet():
        #implementation
        pass

class LandlinePhone(CallingDevice):
    def make_calls():
        #implementation
        pass
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
interface CallingDevice {
    public function make_calls();
}

interface MessagingDevice {
    public function send_sms();
}

interface InternetbrowsingDevice {
    public function browse_internet();
}

class SmartPhone implements CallingDevice, MessagingDevice, InternetbrowsingDevice {
    public function make_calls() {
        // TO DO
    }

    public function send_sms() {
        // TO DO
    }

    public function browse_internet() {
        // TO DO
    }
}

class LandlinePhone implementsCallingDevice {
    public function make_calls() {
        // TO DO
    }
}
]]>
</code-block>
</tab>
</tabs>
