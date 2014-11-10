class: center, middle, inverse

# Other pattern

---

class: middle, center

# Model - Factory method pattern

ActiveRecord (ORM - Object-Relational Mapping)

???

- dostarcza uniwersalną klasę bazową, która sama nie podejmuje decyzji co do tworzonych obiektów (dostarcza tylko interfejs) o sposobie tworzenia decydują podklasy
- przykład obsługa wielu formatów plików graficznych
- .strong[Active Record] po jednej klasie dla każdego adaptera dla każdej bazy danych
- czy zastanawialiście się kto i w jaki sposób zarządza wieloma adapterami?
- .strong[Korzyści:]
- sam zarządza który adapter wybrać
- uniezależnienie kodu

---

class: middle, center

# ActiveSupport - Singleton pattern

Inflections

???

- ogranicza możliwość tworzenia obiektów danej klasy
- tylko jeden obiekt danej klasy, dostęp globalny
- .strong[ActiveSupport] - klasy pomocnicze
- reguły dotyczące tworzenia liczby mnogiej - muszą być tylko raz nie trzeba wielu obiektów
- wykorzystywany tez w Rake - jeden obiekt Rake::Application
- Porównanie do piły - trzeba uważać gdzie i dlaczego to się robi
- uważany czasem za anty wzorzec bo łamie zasady projektowania obiektowego
- często nadużywany lub źle zaimplementowany (nie zrozumiany)
- w Ruby istnieje moduł pomagający stworzyć singleton - .strong[Singleton]

---

class: center, middle, inverse

# Tools

---

class: middle, center

# Generators

.italic[assets, controller, decorator, helper, mailer, migration, model, resource, scaffold, scaffold_controller, ...]

???

- .strong[Korzyści:]
- budują szablony kodu
- cała obsługa CRUD (Create, Read, Update, Delete)
- pokazują schemat poruszania się po aplikacji (umieszczenia kodu w dobrym miejscu)
- automatyzują
- przyśpiesza pisanie kodu
- .strong[Wady:]
- gdy nie jesteśmy zapoznani ze specyfiką działania Rails to może nam się wydawać, że .strong[kod jest poza naszą kontrolą]
- może to być dla nas voodoo

---

class: middle, center

# Rake

DSL - Domain-specific language

???

- .strong[DSL] - język dziedzinowy, dedykowany
- przystosowany do określonej dziedziny problemów, do potrzeb
- dostosowuje używany język do naszych potrzeb
- czasem użytkownik nawet nie wie, że pracuje w danym języku (jest to przed nim ukryte)
- jest to pewien podzbiór języka głównego
- SQL, język wyrażeń regularnych
- .strong[Rake] - odpowiednik narzędzi .strong[make] lub .strong[ant]
- automatyzuje proces kompilacji programów w języku Ruby
- pozwala zarządzać zadaniami, zasobami, bazą danych
- .strong[Korzyści:]
- oddziela zewnętrzne polecenia od samej aplikacji
- cały czas operujemy w obrębie jednego języka

---

class: middle, center

# Bundler

a gem to bundle gems

???

- upewnia się że aplikacja Ruby uruchamia te same środowisko na każdej maszynie
- .strong[gem] - czyli biblioteka
- zarządza wersjami gemów (innych dodatków)
- rozwiązuje zależności między nimi

---

class: middle, center

# Guard

command line tool to easily handle events on file system modifications

???

- narzędzie konsolowe, pozwalające wywoływać zdarzenia na modyfikowanych plikach
- uruchamianie, przeładowywanie serwera po zmianie plików konfiguracyjnych
- przeładowywanie przeglądarki po zmianie css, js, html
- doinstalowywanie gemów
- uruchamianie testów po zapisie zmian w plikach
- .strong[Korzyści:]
- automatyzuje żmudne prace
- pozwala na szybsza pracę

---

class: middle, center

# Sass & Coffee Script

.italic[(.strong[S]yntactically .strong[A]wesome .strong[S]tyle.strong[S]heets)]

???

- ułatwiają pisanie css i js
- przydatne dla programistów z mała świadomością js (bezpieczny dla nich)
- wprowadzanie metod (mixins), zmiennych, zagnieżdżeń do css
- zapamiętywanie kolorów i powtarzających się stylów
- coffee podobnie się pisze jak Ruby

---

class: middle, center

# Tests

Test::Unit & RSpec

???

- ogromny temat, na wiele prezentacji
- .strong[Unit Test] moduł w Ruby, dołączane do Rails
- .strong[RSpec] dodatkowy gem, z bardzo przyjemną składnią (jakby się pisało w języku angielskim)
- same Ralsy zapraszają nas do testowania to dlaczego tego nie robić?
- .strong[TDD] (Test-driven development), .strong[BDD] (Behavior-driven development)
- testy przed kodem
- testy na różnych poziomach (jednostkowe, funkcjonalne, integracyjne)
- gdy mamy dobre testy automatyczne to one są strażnikami naszej aplikacji
- przy dobrych testach refaktoring nie jest problemem
- można zmieniać ulepszać, refaktoryzować kod
