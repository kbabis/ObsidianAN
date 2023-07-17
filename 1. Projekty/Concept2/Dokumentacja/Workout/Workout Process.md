[[2023-04-23]]

#### Cel 🎯
Wytworzenie dwóch rodzajów dokumentacji:
- nietechniczna - ukazuje przebieg procesu,
- techniczna - stanowi wycinki kodu z opisem.

Łączyć je będą sygnatury (w Obsidian przedstawione jako tagi), np. #BT-COMM to część odpowiedzialna za komunikację Bluetooth, a #BT-COMM-1 jednoznacznie identyfikuje metodę `func communication(_ communication: EDBluetoothCommunicating, didReceiveDataUpdate device: EDPMDevice)`.


I. Rozpoczęcie procesu - akcja załadowania widoku
1. wyłączenie idle timera
2. rozpoczęcie inactivity trackera
3. prezentuj widoki treningu w zależności od typu treningu
4. ustaw obserwowanie komunikacji bluetooth #BT-COMM
5. sprawdź, czy kalibracja nie ma miejsca
6. rozpocznij trening na Apple Watch

___

Akcje użytkownika/apple watcha (X)
**X1: Naciśnięcie *Create New Workout* i X2: *Show Logbook***
Jeśli multierg i może wysyłać wirtualne komendy
- A: zakończ trening wirtualnym przyciskiem na PM
- B: zakończ trening (bez rozłączania PMa)

**X3: Naciśnięcie *Disconnect***
- zakończ trening
- rozłącz PM

**X4: Naciśnięcie *Continue Workout***
- wyślij `push virtual key D`

**X5: Zescrollowanie do wybranego widoku treningu**
- nadpisz obecnie wyświetlany ekran treningu\

___
# Level 1 - Interactor

## Input

### System Actions
- viewDidLoad

### User Actions
Menu/Watch:
- didSelectContinueWorkout
- didSelectCreateNewWorkout
- didSelectDisconnect
- didSelectShowLogbookResults

Other:
- didScrollToScreen(type: EDWorkoutScreenType)
- sync popup - retry
- sync popup - cancel
- calibration popup - ok

WorkoutManagingDelegate:
- didCancelWorkoutOnWatch
- workoutDidFail(dueTo:)
- workoutDidFinish(entry:)

## Output
- presenter.presentCreateNew()
- presenter.presentWorkoutDetails(workout:)
- presenter.presentWorkoutScreen(type:)
- presenter.presentSyncingWorkout
- presenter.presentCalibrationPopup
- presenter.presentSyncErrorPopup

# Level 2 - WorkoutWorker
WorkoutManaging

## Input
WorkoutManaging:
- continue
- retry
- start(delegate:)
- stop

Watch:
- watch: didCancelWorkout(dueTo:)
- workoutDidFail(dueTo error: Error, doesAllowRetry: Bool)
- workoutDidFinish(entry: EDWorkoutEntry)

Device:
- didReceive(fixedInterval: EDPMFixedSplitInterval)
- didReceive(fixedSplit: EDPMFixedSplitInterval)
- didReceive(forceCurvePlot: [Int])
- didReceive(rowing: EDPMRowing)
- didReceive(variableInterval: EDPMVariableInterval)
- didReceive(workoutResults: EDPMWorkoutResults)
- didReceive(workoutState: EDPMWorkoutState)
- didReceiveDataUpdate(for device: EDPMDevice)
- didReceiveStrokeChange(for rowing: EDPMRowing)
- didReceiveWorkoutTypeChange(workoutType: EDPMWorkoutType)

Store:
- finished(workout)
- failed(error)

## Output
Interactor:
- workoutDidFinish(entry:)
- workoutDidFail(dueTo:, doesAllowRetry:)
- didCancelWorkoutOnWatch(dueTo:) 

WorkoutHelper (`global`):
- prepareToWorkout()

Output Processing:
    update(fixedSplitInterval: EDPMFixedSplitInterval)
    updateCurvePlot(with input: [Int])
    update(rowing: EDPMRowing)
    updateOnFinish(rowing: EDPMRowing)
    update(variableInterval: EDPMVariableInterval)
    updateStroke(using rowing: EDPMRowing)

Watch:
- resetHeartRate()
- resetSplits()
- startWorkout()
- stopWorkout()

ProcessFeature:
- continue
- retry
- start
- stop
- updateWorkoutTypeUsingDevice
- updateRowing(EDPMRowing)
- updateVariableSplitInterval(EDPMVariableInterval)
- receiveResults(EDPMWorkoutResults)
- updateWorkoutState(EDPMWorkoutState)
- updateDevice(EDPMDevice)
- updateStroke(EDPMRowing)
- updateWorkoutType(EDPMWorkoutType)

