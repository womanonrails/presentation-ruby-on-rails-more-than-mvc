class: center, middle, inverse

# Ruby on Rails - more than MVC
Agnieszka Matysek

---

class: middle

# Agenda
- Ruby on Rails
- Design Patterns in Rails
- Useful tools
- Summary


---

class: center, middle, inverse

# Ruby on Rails

???

- Kto wie czym jest Ruby on Rails?
- .strong[framework open source] do szybkiego tworzenia aplikacji webowych
- stworzony głównie przez duńskiego programistę .strong[Davida Heinemeiera Hanssona (DHH)]
- w ramach pracy nad oprogramowaniem .strong[Basecamp]
- RoR został napisany w języku .strong[Ruby] z użyciem architektury .strong[MVC]

---

class: middle

# Community
- open to people
- open to development
- open to Open Source
- very active

???

- lokalne .strong[grupy Rubiego]: WRUG, SRUG, PRUG, KRUG
- .strong[warsztaty], szkolenia: Rails Girls, Bootcamp (Pilot), netguru workshops
- .strong[konferencje]: ArrrrCamp, wroc_love.rb, RuPy, RailsBerry, EuRuKo, Rails Camp
- .strong[Open Sorce] gem - github
- .strong[tutoriale]: railscasts.com, code schoole, learn street, testing tusday, github

---

class: center, middle, inverse

# Rails vs. Clean Code

???

- dobieranie technologi do potrzeb, do problemu
- co Rails może nam zaproponować w tym temacie?
- czerpanie dobrych wzorców

---

class: center, middle, inverse

# MVC

???

- pierwsza rzecz, najbardziej rzucająca się w oczy
- co to jest MVC?
- .strong[wzorzec projektowy (architektoniczny)] - sprawdzony sposób, przepis na rozwiązanie konkretnego problemu (wiązanego z architekturą oprogramowania)
- służy do organizowania, porządkowania struktury aplikacji z interfejsem graficznym

---

class: middle

.left-column[
# M - Model
### V - View
### C - Controller
]

.right-column[
  .right[
    ![model](./images/model.jpg)
  ]
]

???

- poczta lub silnik
- logika aplikacji
- operacje na danych
- często łączy się z bazą danych

---

class: middle

.left-column[
### M - Model
# V - View
### C - Controller
]

.right-column[
  .right[
    ![view](./images/view.jpg)
  ]
]

???

- dom lub cała karoseria (to jak samochód wygląda)
- wygląd aplikacji
- wyświetla dane w jakimś konkretnym formacie
- mówi jak je wyświetlić (html, xml, json)

---

class: middle

.left-column[
### M - Model
### V - View
# C - Controller
]

.right-column[
  .right[
    ![controller](./images/controller.jpg)
  ]
]

???

- pośrednik miedzy modelem a widokiem
- kurier lub system sterujący
- zarządza zmianami w modelach i aktualizacją (odświeżeniem) widoków

---

class: center, middle, inverse

# Advantages & Disadvantages

???

- .strong[Zalety]
- większa ogólność
- niezależność
- elastyczność rozwiązania
- przejrzystość, zwięzłość, ogólność
- możliwość podmiany np. tylko widoku, tylko w modelu (mechanizm przeliczania wypłat)
- możliwość obsługi różnych typów wizualizacji danych
- mniejsza zależność kodu
- pozwala na odwracalność, piwot, zmianę decyzji
- .strong[Wady]
- by używać trzeba rozumieć
- bariera wejścia
- i tak można to zrobić źle, nieumiejętnie

---

class: middle, center

# Fat Model, Skinny Controller

.small-image[![model & controller](./images/fat-model-skinny-controller.jpg)]

???

- panowała taka zasada w Rails
- można ją spotkać w internecie i literaturze
- nie do końca dobra interpretacja MVC
- kontroler ma być przejrzysty, a wszystko inne ląduje w modelu
- gdzie stosowanie zasady .strong[Single responsibility principle]
- SOLID
- duże modele też nie są dobre!
- rzeczy zaczęły się wymykać z pod kontroli

---

class: center, middle

![Jurassic Park](./images/jurassic-park.jpg)

---

class: center, middle, inverse

# Changes

???

- ludzie się obudzili
- zaczęły się zmiany

---

class: middle

# Rules

- 100 lines per class
- 5 lines per method
- 4 params per method call (and don't even try cheating with hash params)
- 1 instance variables per controller' action
- LoD - Law of Demeter
- KISS - Keep It Simple, Stupid
- DRY - Don't Repeat Yourself
- many, many more

???

- takie rzeczy można sprawdzać dzięki odpowiednim narzędziom - .strong[metryki]
- te zasady to taki trigger do zmian
- gdy narzucamy sobie takie zasady, to dopiero wtedy zaczynamy myśleć
- zaczynamy sięgać po sprawdzone rozwiązania np. wzorce projektowe
- zastanawiamy się czy jest to nam potrzebne?
- czy da się prościej?

---

class: center, middle, inverse

# Simplicity


???

- w wszystkich tych zasadach chodzi o .strong[prostotę], .strong[przejrzystość] i .strong[czytelność]
- jest to istotne bo częściej czytamy kod niż piszemy
- swój kod lub kod innych
- zastanówmy się jak wzorce dają nam Railsy, oto kilka przykładów

---

class: middle, center

# Model - Adapter pattern

ActiveRecord (ORM - Object-Relational Mapping)

![Adapter](./images/adapter.jpg)


???

- .strong[ORM] - sposób odwzorowania obiektowej architektury aplikacji na bazę danych o charakterze relacyjnym
- pozwala na współpracę klas o niekompatybilnych interfejsach
- dodatkowo stworzenie puli takich adapterów o tym samym interfejsie ułatwia sprawę
- .strong[Korzyści:]
- nie jest istotne jaka to baza danych (MySQL, PosgreSQL, SQLite)
- można odłożyć decyzje odnośnie bazy danych na później, możemy łatwo wycofać się z podjętej decyzji
- nie musimy od początku przejmować się niuansami w różnych typach baz danych
- możemy szybko zmienić bazę danych Adaptery zapewniają że odwołania się nie zmienią
- cały mechanizm łączenia z bazą jest poza logiką naszego modelu

---

class: middle, center

# Model - Command pattern

ActiveRecord (Migrations)

???

- .strong[migracje] - sposób na modyfikowanie bazy danych w Rails
- instrukcje realizowania określonych zadań
- zadania mogą być realizowane natychmiast lub nieco później
- mogą być realizowane w kolejności w zależności od innych zadań
- .strong[Korzyści:]
- pamiętanie co się wydarzyło do tej pory
- możliwość cofnięcia zmian
- możliwość modyfikacji wersji bazy danych
- to program wie w jakiej wersji ma bazę, sam dba o to by mieć najnowszą wersję
- automatyzacja powtarzających się procesów
- możliwość dodawania, usuwania, zmieniania elementów bazy danych
- ułatwia współpracę nad projektem każdy wie że coś się zmieniło w bazie, ma kod który mu to zrobi
- nie trzeba gmerać w bazie danych

---

class: middle, center

# Model - Observer pattern

ActiveRecord (Callbacks)

![Observer](./images/observer.jpg)


???

- .strong[collbacks] - wywołania zwrotne, pozwalają wywołać jakąś logikę (kod) przed lub po zmianie stanu obiektu
- .strong[Observer] - używany do powiadamiania zainteresowanych obiektów o zmianie stanu innego obiektu
- .strong[Korzyści:]
- niezależność, ograniczenie związków miedzy modelami (klasami)

---

class: middle, center

# Model - Builder pattern

ActiveRecord (find_by methods)

![Builder](./images/builder.jpg)

???

- wyodrębnia proces tworzenia skomplikowanego obiektu
- może tez zapobiegać tworzeniu nie prawidłowych obiektów
- dzieli proces tworzenia obiektów (skomplikowanych) na kilka mniejszych etapów
- każdy etap może być implementowany na wiele sposobów
- .strong[Active Record] - oferuje możliwość wyszukiwania rekordów w bazie w różny sposób
- wyszukuje w bazie i tworzy obiekt po stronie aplikacji
- User.find_by(name: 'Agnieszka')
- .strong[Korzyści:]
- niezależnie od tego jakie mamy pola w bazie to możemy po nich wyszukiwać dzięki tym metodą
- upraszcza składnie z naszej strony

---

class: middle, center

# ActiveSupport - Decorator pattern

alias_method_chain

![Decorator](./images/decorator.jpg)

???

- Dekorator pozwala na dodanie nowej funkcji do istniejącej klasy (metody) dynamicznie podczas działania programu
- dekorowanie z wykorzystaniem aliasów metod
- alias_method_chain - dekorowanie metod przez wprowadzenie dowolnej liczby funkcji
- nieudekorowana funkcja zmienia nazwę a udekorowana przyjmuje nazwę wcześniejszej funkcji
- .strong[Korzyści:]
- dalej używamy tej samej nazwy metody ale ma ona super właściwości w określonych momentach
- nie musimy pisać swoich klas dopisujących dodatkowe rzeczy do już istniejących klas np. Array zamiast NewArray
- nie musimy korzystać z dziedziczenia na różne warianty klasy
- jedna klasa plus zbiór dekoratorów do tej klasy
- warstwowa konstrukcja: najpierw podstawowe funkcjonalności a później szczegółowe
- izolacja
- .strong[Wady:]
- trzeba to ostrożnie używać

 ---

class: middle, center

# Controller - Strategy pattern

render (HTML, XML, json, ...)

![Strategy](./images/strategy.jpg)

???

- wymienne stosowanie algorytmu w trakcie działania aplikacji niezależnie od korzystających z nich klientów
- Proc - bloki kodu np. sortowanie tablicy
- format.html, format.xml, format.js, ...
- działania algorytmu wskazane są obiektowi w zależności od kontekstu różnych obiektów strategii

---

class: middle, center

# Model - Meta-programming

attr_accessor, attr_reader, attr_writer

???

- dostęp do obiektów z wykorzystaniem mechanizmów dynamicznych
- kod piszący kod
- tworzenie kody za pomocą kodu w trakcie działania programu (systemu)
- przykład - has_one, has_many (ActiveRecord)
- .strong[Korzyści:]
- elastyczność metod, klas czy modułów
- skraca kod
- upraszcza go
- jest podstawą do wzorca DSL, o którym będę mówić później

---

class: middle, center

# Convention Over Configuration

Ruby on Rails

???

- konwencja nad konfiguracją
- większy rozmach tego wzorca
- koncentruje się na łączeniu całych aplikacji
- dzięki temu można napisać swój fragment funkcjonalności lub taką pod aplikację .strong[engine] i wszystko działa po dołączeniu do innych aplikacji (w uproszczeniu - czasem jest jeszcze potrzebna zgodność wersji np. Rubiego)
- złożone rozwiązania z użyciem niewielkiej ilości kodu
- Jak zaprojektować architekturę frameworku lub aplikacji by była łatwo rozszerzalna?
- przesadzanie z możliwością konfigurowania (Servlety Javy)
- zachowanie rozszerzalności i nie przeładowywanie konfiguracją
- .strong[Zasady:]
- Przewidywanie potrzeb użytkownika - standardowe zadania wymagają mało pracy, niestandardowe więcej
- Nie zmuszaj do wykonywania ponownie danej decyzji - czy jesteś pewien? - budowanie konwencji umieszczania elementów zamiast ciągłe pytanie o konfiguracje
- Opracuj początkowy szablon np. gemu, aplikacji (scaffold)
- przykłady konwencji, gdzie pliki dla konkretnych elementów kontroler, widok, model
- czy można to zmienić? oczywiście! Ale po co się męczyć?

---


class: center, middle

.large-image[![Apollo 13](./images/apollo13.jpg)]

---

class: middle, inverse

# Other tools

- Generators
- Rake
- Bundler
- Guard
- Sass & Coffee Script
- Tests


???

- narzędzia, które ułatwiają nam kodzenie
- robią pewne rzeczy za nas


- .strong[Generatory]
- budują szablony kodu
- cała obsługa CRUD (Create, Read, Update, Delete)
- pokazują schemat poruszania się po aplikacji (umieszczenia kodu w dobrym miejscu)
- automatyzują, przyśpiesza pisanie kodu


- .strong[Rake] - odpowiednik narzędzi .strong[make] lub .strong[ant]
- automatyzuje proces kompilacji programów w języku Ruby
- pozwala zarządzać zadaniami, zasobami, bazą danych


- .strong[Bundler]
- upewnia się że aplikacja Ruby uruchamia te same środowisko na każdej maszynie
- zarządza wersjami gemów (innych dodatków)
- rozwiązuje zależności między nimi


- .strong[Guard]
- narzędzie konsolowe, pozwalające wywoływać zdarzenia na modyfikowanych plikach
- uruchamianie, przeładowywanie serwera po zmianie plików konfiguracyjnych
- przeładowywanie przeglądarki po zmianie css, js, html
- doinstalowywanie gemów
- uruchamianie testów po zapisie zmian w plikach


- .strong[Sass & Coffee Script]
- ułatwiają pisanie css i js
- przydatne dla programistów z mała świadomością js (bezpieczny dla nich)
- wprowadzanie metod (mixins), zmiennych, zagnieżdżeń do css
- zapamiętywanie kolorów i powtarzających się stylów
- coffee podobnie się pisze jak Ruby


- .strong[Testy]
- ogromny temat
- .strong[Unit Test] moduł w Ruby, dołączane do Rails
- .strong[RSpec] dodatkowy gem, z bardzo przyjemną składnią (jakby się pisało w języku angielskim)
- same Ralsy zapraszają nas do testowania to dlaczego tego nie robić?
- .strong[TDD] (Test-driven development), .strong[BDD] (Behavior-driven development)
- testy przed kodem
- testy na różnych poziomach (jednostkowe, funkcjonalne, integracyjne)
- gdy mamy dobre testy automatyczne to one są strażnikami naszej aplikacji
- przy dobrych testach refaktoring nie jest problemem
- można zmieniać ulepszać, refaktoryzować kod

---

class: middle, inverse

# Summary

- good code is writing by good programmers
- code responsibility
- learn all the time
- sometimes you make mistake
- develop your skills

???

- polecam zainteresować się wzorcami projektowymi
- testowanie jako obowiązek i przyjemność (pewnik niezawodności systemu, utrzymania)
- świadomi programiści, otwarci na nowe rozwiązania
- nie akceptujcie niedoróbek w projekcie
- niezależność elementów
- dobrze opanuj narzędzia z którymi pracujesz
- czy jest mi to potrzebne? czy da się prościej?
- mam nadzieję że uda Wam się wykorzystać choćby jedną małą rzecz, czerpiąc z Rails by udoskonalić swój projekt, swoja aplikację

---

class: center, middle

# Questions?

---

class: middle, inverse

# Bibliography

- [Let’s talk about SRP in models](http://vimeo.com/98198895)
- [Odchudzanie ActiveRecord](http://vimeo.com/94329799)
- [Form Objects](http://railscasts.com/episodes/416-form-objects)
- [Sandi Metz' Rules For Developers](http://robots.thoughtbot.com/sandi-metz-rules-for-developers)
- [sandi_meter](https://github.com/makaroni4/sandi_meter)
- [Baruco 2013: Rules, by Sandi Metz](http://www.youtube.com/watch?v=npOGOmkxuio)
- [The Pragmatic Programmer: From Journeyman to Master](http://www.amazon.com/exec/obidos/ASIN/020161622X)
- [Design Patterns in Ruby](http://www.amazon.com/exec/obidos/ASIN/0321490452)
- [Code School](https://www.codeschool.com/)
- [Rails Documentation](http://api.rubyonrails.org/)
- [Reek](https://github.com/troessner/reek/wiki)
- [RuboCop](https://github.com/bbatsov/rubocop)
- [Bundler](https://github.com/bundler/bundler)
- [Guard](https://github.com/guard/guard)
- [Coffee Script](http://coffeescript.org/)
- [SASS](http://sass-lang.com/)
- [RSpec](https://github.com/rspec/rspec)

---

class: middle, center

.small-image[![Womanonrails](./images/womanonrails.png)]
### Agnieszka Matysek
[@womanonrails](https://twitter.com/womanonrails)

amatysek@fractalsoft.org

