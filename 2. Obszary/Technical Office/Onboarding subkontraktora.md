[[2023-07-04]]
___
[[2023-07-05]]
1. Wymagania projektowe i zapotrzebowanie  
   1.1. zapoznanie się z wymaganiami dotyczącymi projektu  
   1.2. ustalenie wymagań (technologie, cechy)  
2. [Opcjonalnie] Wybór kandydata  
3. Rekrutacja techniczna  
   - max. 30 minut  
   - osoba z zespołu weryfikacyjnego + developer z projektu (jeśli brak, PM)  
4. Pomoc w setupie projektu  
   - [Opcjonalnie] dodanie do [ios-pr-crew](https://angrynerds-pl.slack.com/archives/GJ78GSP8E)  
   - niezbędny dostęp do przestrzeni projektowej w DevOps i do Harvest  
   - przedstawienie praktyk w AN  
   - ustalenie stacku technologicznego  
5. Nadzorowanie postępów projektu  
   - przeglądanie PRek  
   - kontakt z PM na temat postępów

Aktorzy:
- Kontraktor - programista z zewnętrznej firmy, który dołącza do projektu
- LM - menedżer liniowy
- PM - menedżer projektu
- TO - członek/członkowie zespołu Technical Office
- TV - członek/członkowie zespołu weryfikacji technicznej
- Developer - programista z AN, który będzie współprowadził projekt z [Kontraktor]


1. Wymagania projektowe i określenie zapotrzebowania
Projekt zostanie przedstawiony [TO] przez [LM]a/[PM]a w formie wymagań dotyczących aplikacji, na których podstawie [TO] określi wymagany poziom umiejętności potrzebny do realizacji zadania i wskaże oczekiwaną liczbę osób potrzebną do realizacji zadań. Wstępnie określony zostanie stos technologiczny, co pozwoli doprecyzować listę kryteriów podczas poszukiwania kandydatów.

2. < Opcjonalnie > Wybór kandydata
Celem oszczędności czasu na etapie rozmów i dobrania jak najlepszego kandydata na wstępnym etapie,[TO]/[TV] przegląda listę dostępnych CV i pomaga odsiać te, w których umiejętności i doświadczenie są najmniej dopasowane do projektu.

3. Rekrutacja techniczna
- krótki czas trwania (max. 30 min) - rekrutacje kontraktorów nie powinny być tak czasochłonne jak standardowe, a w półgodzinnym bloku [TV] w znakomitej większości przypadków w stanie sprawdzić, czy kandydat jest w stanie podołać zadaniu realizacji projektu.
- skład zespołu weryfikacyjnego - pierwszą osobą będzie stanowić [TV], który wykorzysta swoje doświadczenie w procesie weryfikacji, a wspomoże go osoba z wiedzą domenową, którą będzie:
	- [Developer] oceniający głównie, czy chciałby współpracować z kandydatem. Jeśli
	- [PM], jeśli [Kontraktor] ma stanowić jedynego programistę w projekcie.

4. Setup projektu
Jednym z głównych akceleratorów projektu jest jego dobry start, dlatego tu swoim doświadczeniem posłuży [TO] pomagając postawić projekt. Dzięki temu łatwiej będzie również wprowadzić stosowane przez AN praktyki.

Składa się to z następujących kroków:
- [PM] przydziela dostęp do przestrzeni projektowej w DevOps i do Harvest dla [TO],
- [TO] ustala z [Kontraktor] (i może z [PM]) stos technologiczny projektu,
- [TO] pomaga w setupie projektu i przedstawia praktyki stosowane w AN dotyczące m.in.:
	  - systemu kontroli wersji git, git flow, reguł zatwierdzania zmian,
	  - zasad tworzenia, przeglądania i akceptacji Pull Requestów,
	  - stosowanych narzędzi (Tuist, swiftlint itd.),
- < Opcjonalnie > [TO] dodaje projekt do [ios-pr-crew](https://angrynerds-pl.slack.com/archives/GJ78GSP8E) .

5. Nadzorowanie postępów
- [TO] przegląda zmiany w kodzie, akceptuje pierwsze Pull Requesty i konsultuje się z [Kontraktor] na temat zmian,
- [TO] konsultuje się z [PM] na temat postępów.

____
[[2023-07-04]]
Tomek pisze:
> *[@Paulina Drożdż](https://angrynerds-pl.slack.com/team/U04JWH3ELCU) przypomniała mi, że tworzyła niedawno opis procesu onboardingowego dla kontraktorów, także możesz od tego wyjść:
> 
> **Onboarding subkontraktora**  

1. Dopilnowanie podpisania dokumentów z agencją, proces wykonuje Wiktoria Kipczak.
2. Przesłanie prośby HR o przygotowanie dostępów dla subkontraktora [imię i nazwisko, firma]

1. e-mail w domenie AN + dostęp do Harvest

1. Przesłanie dostępów do kandydata

1. instrukcja zalogowania się na nowe konto e-mail + informacja o pierwszym dniu

1. Dodanie subkontraktora do Slacka jako “guest” do wybranego kanału projektowego. W tym celu LM musi być dodany do tego kanału (nawet na chwilę).
2. Dodanie do Azure DevOps, jeśli projekt korzysta z softu po stronie AN. Jeśli nie, to przesłanie prośby o dodanie do softu klienta przez PM lub DM projektu.
3. Zaimportowanie konta z Harvest do Forecast.
4. Poinformowanie PMa o szczegółach związanych z pierwszym dniem pracy subkontraktora.
5. Spotkanie “Let’s meet” pierwszego dnia pracy

1. krótki wstęp o firmie, ograniczonym dostępie do systemów AN dla subkontraktorów, perspektywie projektu i struktury organizacyjnej PM/DM/LM. W tym LM jako osoba do eskalacji.

1. wprowadzenie do Harvest, zasad związanych z logowaniem czasu pracy i zgłaszaniem urlopów [może być zdelegowane na PMa projektu]

1. informacja o specjalnych zasadach logowania np. niebillowalny okres onboardingu, jeśli został taki ustalony*
___
## Moje notatki

Onboarding osób technicznych  
- rozmowa rekrutacyjna ma mieć miejsce, może w nieco lżejszym wydaniu
- osoba przechodzi przez ręce TO - spisać zasady panujące w firmie

Etapy:
1. Przegląd wymagań (i projektu)
2. Rekrutacja techniczna [1 x team weryfikacyjny, 1 x team techniczny z projektu / PM]
3. Onboarding
4. Pomoc przy stawianiu projektu
5. Wsparcie na dalszych etapach