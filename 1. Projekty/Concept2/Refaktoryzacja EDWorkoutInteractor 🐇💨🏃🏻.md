[[2023-04-21]]
`Developer/Concept2/Dokumentacja/EDWorkoutFeature`

1. Znalezienie wersji `EDWorkoutInteractor` do porównania. Wersji kodu z którego dnia używałem do implementacji `EDWorkoutFeature`? Trochę się od tamtego czasu pozmieniało.

[Wersja](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_git/hsl-concept2-ergdata-ios/commit/d672d79dbacd93f244595bf82a92674cadaff62d?refName=refs/heads/feature/84631-workout-feature-adjustments) z [[2023-03-20]] powinna się nadać.

#### [[2023-03-13]] 
Wprowadzałem dalsze zmiany na branchu [feature/84631-workout-feature-adjustments](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_git/hsl-concept2-ergdata-ios?version=GBfeature/84631-workout-feature-adjustments) jako część zadania [#84631 | Test workouts using EDWorkoutFeature](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_workitems/edit/84631).
Dodałem:
- wsparcie dla audio guidance,
- `EDWorkoutError`,
- mechanizm `retry`,
- analitykę (`EDWorkoutAnalyzer`),
- zastąpiłem `EDWorkoutBuilder` i `EDWorkoutInteractor` nowszymi wersjami.

#### [[2023-01-11]] 
Utworzyłem pull request [#37848 | Refactor the workout module](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_git/hsl-concept2-ergdata-ios/pullrequest/37848) na podstawie brancha [feature/81814-workout-module-refactor](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_git/hsl-concept2-ergdata-ios?version=GBfeature/81814-workout-module-refactor) powiązanego z ticketem [#81814 | Refactor PM communication module](https://dev.azure.com/angrynerds/Devscale%20-%20Concept2/_workitems/edit/81814/)

2. Pobrałem 3 wersje interaktora:
	- poprzednią z [[2023-03-16]],
	- poprzednią z [[2023-03-16]] z komentarzami objaśniającymi w stashu,
	- obecną.
Będę porównywać 1 i 3 w *Visual Studio Code* (`cmd + shift + P` > `Compare with...`).

