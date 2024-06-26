# Введение

## Что такое Паттерн?

**Паттерн проектирования** — это часто встречающееся решение определённой проблемы при проектировании архитектуры программ.

В отличие от готовых функций или библиотек, паттерн нельзя просто взять и скопировать в программу. Паттерн представляет собой не какой-то конкретный код, а общую концепцию решения той или иной проблемы, которую нужно будет ещё подстроить под нужды вашей программы.

Паттерны часто путают с алгоритмами, ведь оба понятия описывают типовые решения каких-то известных проблем. Но если алгоритм — это чёткий набор действий, то паттерн — это высокоуровневое описание решения, реализация которого может отличаться в двух разных программах.

Если привести аналогии, то алгоритм — это кулинарный рецепт с чёткими шагами, а паттерн — инженерный чертёж, на котором нарисовано решение, но не конкретные шаги его реализации.

### Из чего состоит паттерн?

Описания паттернов обычно очень формальны и чаще всего состоят из таких пунктов:

- проблема, которую решает паттерн;
- мотивации к решению проблемы способом, который предлагает паттерн;
- структуры классов, составляющих решение;
- примера на одном из языков программирования;
- особенностей реализации в различных контекстах;
- связей с другими паттернами.

Такой формализм в описании позволил создать обширный каталог паттернов, проверив каждый из них на состоятельность.

## История паттернов

Кто придумал паттерны? Это хороший, но не совсем корректный вопрос, так как паттерны не придумывают, а, скорее, «открывают». Это не какие-то супер-оригинальные решения, а наоборот, часто встречающиеся, типовые решения одной и той же проблемы.

Концепцию паттернов впервые описал Кристофер Александер в книге «[Язык шаблонов. Города. Здания. Строительство](https://www.artlebedev.ru/izdal/yazyk-shablonov/)». В книге описан «язык» для проектирования окружающей среды, единицы которого — шаблоны (или паттерны, что ближе к оригинальному термину patterns) — отвечают на архитектурные вопросы: какой высоты сделать окна, сколько этажей должно быть в здании, какую площадь в микрорайоне отвести под деревья и газоны.

Идея показалась заманчивой четвёрке авторов: Эриху Гамме, Ричарду Хелму, Ральфу Джонсону, Джону Влиссидесу. В 1994 году они написали книгу «[Приемы объектно-ориентированного проектирования. Паттерны проектирования](https://ozon.ru/t/aorokMM)», в которую вошли 23 паттерна, решающие различные проблемы объектно-ориентированного дизайна. Название книги было слишком длинным, чтобы кто-то смог всерьёз его запомнить. Поэтому вскоре все стали называть её «book by the gang of four», то есть «книга от банды четырёх», а затем и вовсе «GoF book».

С тех пор были найдены десятки других объектных паттернов. «Паттерновый» подход стал популярен и в других областях программирования, поэтому сейчас можно встретить всевозможные паттерны и за пределами объектного проектирования.

## Зачем знать паттерны?

Вы можете вполне успешно работать, не зная ни одного паттерна. Более того, вы могли уже не раз реализовать какой-то из паттернов, даже не подозревая об этом.

Но осознанное владение инструментом как раз и отличает профессионала от любителя. Вы можете забить гвоздь молотком, а можете и дрелью, если сильно постараетесь. Но профессионал знает, что главная фишка дрели совсем не в этом. Итак, зачем же знать паттерны?

- **Проверенные решения.** Вы тратите меньше времени, используя готовые решения, вместо повторного изобретения велосипеда. До некоторых решений вы смогли бы додуматься и сами, но многие могут быть для вас открытием.

- **Стандартизация кода.** Вы делаете меньше просчётов при проектировании, используя типовые унифицированные решения, так как все скрытые проблемы в них уже давно найдены.

- **Общий программистский словарь.** Вы произносите название паттерна, вместо того, чтобы час объяснять другим программистам, какой крутой дизайн вы придумали и какие классы для этого нужны.

## Критика паттернов

Паттерны были описаны более 20-ти лет назад, поэтому только ленивый не успел бросить в них камень. Давайте рассмотрим самую популярную критику.

### Костыли для слабого языка программирования

> Впервые эту точку зрения выразил Пол Грэм в эссе «[Месть Ботанов](https://habrahabr.ru/post/267865/)». Подробней об этой точке зрения — [Wiki](http://wiki.c2.com/?AreDesignPatternsMissingLanguageFeatures)

Нужда в паттернах появляется тогда, когда люди выбирают для своего проекта язык программирования с недостаточным уровнем абстракции. В этом случае, паттерны — это костыль, который придаёт этому языку суперспособности.

Например, паттерн **Стратегия** в современных языках можно реализовать простой анонимной (лямбда) функцией.

### Неэффективные решения

Паттерны пытаются стандартизировать подходы, которые и так уже широко используются. Эта стандартизация кажется некоторым людям догмой и они реализуют паттерны «как в книжке», не приспосабливая паттерны к реалиям проекта.

### Неоправданное применение

> Если у тебя в руках молоток, то все предметы вокруг начинают напоминать гвозди.
{style="note"}

Похожая проблема возникает у новичков, которые только-только познакомились с паттернами. Вникнув в паттерны, человек пытается применить свои знания везде. Даже там, где можно было бы обойтись кодом попроще.

## Классификация паттернов

Паттерны отличаются по уровню сложности, детализации и охвата проектируемой системы. Проводя аналогию со строительством, вы можете повысить безопасность перекрёстка, поставив светофор, а можете заменить перекрёсток целой автомобильной развязкой с подземными переходами.

Самые низкоуровневые и простые паттерны — идиомы. Они не универсальны, поскольку применимы только в рамках одного языка программирования.

Самые универсальные — *архитектурные паттерны*, которые можно реализовать практически на любом языке. Они нужны для проектирования всей программы, а не отдельных её элементов.

Кроме того, паттерны отличаются и предназначением. В этой книге будут рассмотрены три основные группы паттернов:

- **[Порождающие паттерны](creational-patterns.md)** беспокоятся о гибком создании объектов без внесения в программу лишних зависимостей.
- **[Структурные паттерны](structural-patterns.md)** показывают различные способы построения связей между объектами.
- **[Поведенческие паттерны](behavioral-patterns.md)** заботятся об эффективной коммуникации между объектами.