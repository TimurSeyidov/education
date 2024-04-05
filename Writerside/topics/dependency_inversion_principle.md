# Принцип инверсии зависимостей

Принцип инверсии зависимостей гласит:
1. Модуль высокого уровня не должен зависеть от модулей низкого уровня. И то, и другое должно зависеть от абстракций.
2. Абстракции не должны зависеть от деталей реализации. Детали реализации должны зависеть от абстракций.

Если ваш код уже реализует принципы открытости/закрытости и подстановки Лисков, он уже будет неявно согласован с принципом инверсии зависимостей.  
Следуя принципу открытости/закрытости, вы создаете интерфейсы, которые можно использовать для предоставления различных высокоуровневых реализаций. Следуя принципу подстановки Лисков, вы гарантируете, что сможете заменить экземпляры класса низкого уровня объектами класса высокого уровня без какого-либо негативного воздействия на приложение. Таким образом, следуя этим двум принципам, вы гарантируете, что ваши классы высокого уровня и классы низкого уровня зависят от интерфейсов. Следовательно, вы неявно следуете принципу инверсии зависимостей.
Как показано в коде ниже, у нас есть класс `Student`, который мы используем для создания экземпляров `Student` и класса `TeamMemberships`, который содержит сведения о принадлежности учеников к разным командам.
Теперь мы определим высокоуровневый класс `Analysis`, где нам нужно отсеять всех учеников, принадлежащих красной команде.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from enum import Enum
from abc import ABCMeta, abstractmethod

class Teams(Enum):
    BLUE_TEAM = 1
    RED_TEAM = 2
    GREEN_TEAM = 3

class Student:
    def __init__(self, name):
        self.name = name

class TeamMemberships():
    def __init__(self):
        self.team_memberships = []

    def add_team_memberships(self, student, team):
        self.team_memberships.append((student, team))

class Analysis():
    def __init__(self, team_student_memberships):
        memberships = team_student_memberships.team_memberships
        for members in memberships:
            if members[1] == Teams.RED_TEAM:
                print(f'{members[0].name} is in RED team')


student1 = Student('Ravi')
student2 = Student('Archie')
student3 = Student('James')

team_memberships = TeamMemberships()
team_memberships.add_team_memberships(student1, Teams.BLUE_TEAM)
team_memberships.add_team_memberships(student2, Teams.RED_TEAM)
team_memberships.add_team_memberships(student3, Teams.GREEN_TEAM)

Analysis(team_memberships)
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
enum Teams
{
    case BLUE_TEAM;
    case RED_TEAM;
    case GREEN_TEAM;
}

class Student {
    public string $name;

    public function __construct(string $name) {
        $this->name = $name;
    }
}

class TeamMemberships {
    public array $team_memberships = [];

    public function add_team_memberships(Student $student, Teams $team) {
        $this->team_memberships[] = [$student, $team];
    }
}

class Analysis {
    public function __construct(TeamMemberships $team_student_memberships) {
        $memberships = $team_student_memberships->team_memberships;
        foreach ($memberships as $member) {
            if ($member[1] === Teams::RED_TEAM) {
                echo $member[0]->name . ' is in RED team';
            }
        }
    }
}

$student1 = new Student('Ravi');
$student2 = new Student('Archie');
$student3 = new Student('James');

$team_memberships = new TeamMemberships();
$team_memberships->add_team_memberships($student1, Teams::BLUE_TEAM);
$team_memberships->add_team_memberships($student2, Teams::RED_TEAM);
$team_memberships->add_team_memberships($student3, Teams::GREEN_TEAM);

new Analysis($team_memberships);
]]>
</code-block>
</tab>
</tabs>

```bash
Archie is in RED team
```

Как видно из реализации, мы напрямую используем `team_student_memberships`.`team_memberships` в высокоуровневом классе `Analysis`, и мы используем реализацию этого списка непосредственно в классе высокого уровня. На данный момент все нормально, но представьте ситуацию, в которой нам нужно изменить эту реализацию со списка на что-то другое. В этом случае наш класс высокого уровня `Analysis` сломается, поскольку он зависит от деталей реализации `TeamMemberships` низкого уровня.
Теперь взгляните на пример ниже, в котором мы меняем эту реализацию и приводим ее в соответствие с принципом инверсии зависимостей.

<tabs>
<tab title="Python">
<code-block lang="python">
<![CDATA[
from enum import Enum
from abc import ABCMeta, abstractmethod

class Teams(Enum):
    BLUE_TEAM = 1
    RED_TEAM = 2
    GREEN_TEAM = 3


class TeamMembershipLookup():
    @abstractmethod
    def find_all_students_of_team(self, team):
        pass

class Student:
    def __init__(self, name):
        self.name = name

class TeamMemberships(TeamMembershipLookup):
    def __init__(self):
        self.team_memberships = []

    def add_team_memberships(self, student, team):
        self.team_memberships.append((student, team))

    def find_all_students_of_team(self, team):
        for members in self.team_memberships:
            if members[1] == team:
                yield members[0].name   

class Analysis():
    def __init__(self, team_membership_lookup):
        for student in team_membership_lookup.find_all_students_of_team(Teams.RED_TEAM):
            print(f'{student} is in RED team.')


student1 = Student('Ravi')
student2 = Student('Archie')
student3 = Student('James')

team_memberships = TeamMemberships()
team_memberships.add_team_memberships(student1, Teams.BLUE_TEAM)
team_memberships.add_team_memberships(student2, Teams.RED_TEAM)
team_memberships.add_team_memberships(student3, Teams.GREEN_TEAM)

Analysis(team_memberships)
]]>
</code-block>
</tab>
<tab title="PHP">
<code-block lang="php">
<![CDATA[
enum Teams
{
    case BLUE_TEAM;
    case RED_TEAM;
    case GREEN_TEAM;
}

interface TeamMembershipLookup {
    public function find_all_students_of_team(Teams $team);
}

class Student {
    public string $name;

    public function __construct(string $name) {
        $this->name = $name;
    }
}

class TeamMemberships implements TeamMembershipLookup {
    private array $team_memberships = [];

    public function add_team_memberships(Student $student, Teams $team) {
        $this->team_memberships[] = [$student, $team];
    }

    public function find_all_students_of_team(Teams $team) {
        return array_map(
            function ($item) {
                return $item[0]->name;
            },
            array_filter(
                $this->team_memberships,
                function ($item) use ($team) {
                    return $item[1] === $team;
                }
            )
        );
    }
}

class Analysis {
    public function __construct(TeamMemberships $team_student_memberships) {
        $memberships = $team_student_memberships->find_all_students_of_team(Teams::RED_TEAM);
        foreach ($memberships as $member) {
            echo $member . ' is in RED team';
        }
    }
}

$student1 = new Student('Ravi');
$student2 = new Student('Archie');
$student3 = new Student('James');

$team_memberships = new TeamMemberships();
$team_memberships->add_team_memberships($student1, Teams::BLUE_TEAM);
$team_memberships->add_team_memberships($student2, Teams::RED_TEAM);
$team_memberships->add_team_memberships($student3, Teams::GREEN_TEAM);

new Analysis($team_memberships);
]]>
</code-block>
</tab>
</tabs>

```bash
Archie is in RED team
```

Чтобы следовать принципу инверсии зависимостей, нам необходимо убедиться, что класс высокого уровня `Analysis` не зависит от конкретной реализации класса низкого уровня `TeamMembership`. Вместо этого он должен зависеть от некоторой абстракции.
Итак, мы создаем интерфейс `TeamMembershipLookup`, который содержит абстрактный метод `find_all_students_of_team`, передающийся любому классу, наследующему этот интерфейс. Мы наследуем наш класс `TeamMembership` от этого интерфейса, следовательно, теперь класс `TeamMembership` должен предоставлять реализацию функции `find_all_students_of_team`. Затем эта функция передает результаты любому другому вызывающему ее объекту. Мы перенесли обработку, которая делалась в классе высокого уровня `Analysis` в `TeamMemberships` через интерфейс `TeamMembershipLookup`.
Сделав все это, мы убрали зависимость класса `Analysis` от класса `TeamMemberships` и перенесли ее в интерфейс `TeamMembershipLookup`. Теперь класс высокого уровня не зависит от деталей реализации класса низкого уровня. Любые изменения в деталях реализации класса низкого уровня не влияют на класс высокого уровня.