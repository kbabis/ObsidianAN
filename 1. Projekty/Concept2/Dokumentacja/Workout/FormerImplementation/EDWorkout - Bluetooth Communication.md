[[2023-04-24]]
💬 
> Pomocny okazał się cyfrowy inteligentny przyjaciel, który pomógł w generowaniu dokumentacji.

Wygeneruj nietechniczną dokumentację w języku angielskim w formacie Markdown do poniższego kodu na podstawie przykładu.

Kod:
```swift
// kod
```
Przykład:
```
The `communication(_:didReceiveDataUpdate:)` method is called when data is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by retrieving the workout duration, workout type, and updating the workout settings.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `device`: `EDPMDevice` - the PM device that sent the data

### Details
1.  Check if the workout is in the Just Row mode, retrieve the workout duration, and update the `elapsedTime` variable.
2.  Check if the device is in the middle of a workout and the workout is not in the process of stopping.
3.  Update the workout type and store the original workout type to compare with the final workout type. Update the workout type in `workout`.
4.  Update information about the connected device and workout settings in `workout`.
```
___

Bluetooth communication module #BT-COMM  provides the following functions:
1. `communication(_ communication: EDBluetoothCommunicating, didReceiveDataUpdate device: EDPMDevice)`
2. `communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutState state: EDPMWorkoutState)`
3. `communication(_ communication: EDBluetoothCommunicating,didReceiveWorkoutTypeChange workoutType: EDPMWorkoutType)`
4. `communication(_ communication: EDBluetoothCommunicating, didReceiveRowing rowing: EDPMRowing)`
5. `communication(_ communication: EDBluetoothCommunicating, didReceiveFixedSplit split: EDPMFixedSplitInterval)`
6. `communication(_ communication: EDBluetoothCommunicating,  didReceiveFixedInterval interval: EDPMFixedSplitInterval)`
7. `communication(_ communication: EDBluetoothCommunicating,didReceiveVariableInterval variable: EDPMVariableInterval)`
8. `communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutResults results: Result<EDPMWorkoutResults, Error>)`
9. `communication(_ communication: EDBluetoothCommunicating, didReceiveStrokeChange rowing: EDPMRowing)`
10. `communication(_ communication: EDBluetoothCommunicating, didReceiveForceCurvePlot plot: [Int])`
11. `communication(_ communication: EDBluetoothCommunicating, didFail error: EDPMCommunicationError)`
12. `communication(_ communication: EDBluetoothCommunicating, didReceiveMessage message: [Int], error: Int)`
13. `communication(_ communication: EDBluetoothCommunicating, didSend message: [Int])`


## #BT-COMM-1 `communication(_:didReceiveDataUpdate:)`

The `communication(_:didReceiveDataUpdate:)` method is called when data is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by retrieving the workout duration, workout type, and updating the workout settings.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `device`: `EDPMDevice` - the PM device that sent the data

### Details
1.  Check if the workout is in the Just Row mode, retrieve the workout duration, and update the `elapsedTime` variable.
2.  Check if the device is in the middle of a workout and the workout is not in the process of stopping.
3.  Update the workout type and store the original workout type to compare with the final workout type. Update the workout type in `workout`.
4.  Update information about the connected device and workout settings in `workout`.

### Path
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
3. `EDPMCommunication.receivedDataUpdate(from device: PMDevice!)`
	↴
4. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveDataUpdate device: EDPMDevice)`

## #BT-COMM-2 `communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutState state: EDPMWorkoutState)`

The `communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutState state: EDPMWorkoutState)`function is called when the workout state changes. This function updates the workout state and checks if the workout has finished, stopped, or is in the process of being calibrated.

### Arguments
-   `state`: `EDPMWorkoutState` - the new workout state

### Details
1.  Log a debug message about the new workout state.
2.  Check if the workout is not in the process of being calibrated.
3.  Log the termination mode based on the new workout state.
4.  If the workout has been logged and is not in the process of stopping, set the active finishing reason, do not close the screen after sync, and stop the workout.
5.  If the workout is not in progress, not finished, and is not stopping, stop the workout.
6.  If the workout is not in progress, not finished, and is a fixed interval workout, stop the workout.
7.  Update the last workout state.

### Paths
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `rowingSummary - `CE060039-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.workoutSummaryUpdate`
	↴
3. `EDDataPMBleConnection.saveWorkoutSummaryForDeviceWithSerialNumber`
    ↴
4. `EDPMCommunication.receivedWorkoutStateChange(from device: PMDevice!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveDataUpdate device: EDPMDevice)`

or

1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
3. `EDPMCommunication.receivedWorkoutStateChange(from device: PMDevice!)`
	↴
4. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveDataUpdate device: EDPMDevice)`

## #BT-COMM-3 `communication(_ communication: EDBluetoothCommunicating,didReceiveWorkoutTypeChange workoutType: EDPMWorkoutType)`

This function is called when the Bluetooth communication receives a workout type change from the connected device. The function updates the workout type in the `workout` object.

### Arguments
-   `communication`: an instance of `EDBluetoothCommunicating` class that is responsible for Bluetooth communication with the connected device.
-   `workoutType`: an instance of `EDPMWorkoutType` class representing the new workout type received from the connected device.

### Details
1.  Check if the workout is currently in progress and is not being stopped.
2.  Update the workout type based on the new received workout type.

### Path
Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`

1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
3. `EDPMCommunication.receivedWorkoutTypeChange(from device: PMDevice!)`
	↴
4. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating,didReceiveWorkoutTypeChange workoutType: EDPMWorkoutType)`


## #BT-COMM-4 `communication(_ communication: EDBluetoothCommunicating, didReceiveRowing rowing: EDPMRowing)`
The function is called when a new rowing data is received from the connected Bluetooth device. 

### Arguments
-   `communication`: an object conforming to the `EDBluetoothCommunicating` protocol representing the Bluetooth communication layer.
-   `rowing`: an object conforming to the `EDPMRowing` protocol representing the current rowing data.

### Details
1.  Check if the calibration is in progress. If so, return without doing anything else.
2.  Update the table with the new rowing data if the table worker's delegate is set. Also update the stroke count.
3.  Set the `isMultiErg` flag based on the extra rowing status received. Also set the `isAbleToSendVirtualCommands` flag based on the machine type's firmware version.
4.  If the workout is an interval workout and the split or interval count has changed, resize the current points on the graph screen.
5.  Update the split or interval count based on the new rowing data.
6.  If the rowing status indicates that the workout has finished, calculate the graph with the new rowing data on the graph screen.

### Path
Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`

1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `rowingStatus` - `CE060031-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
3. `EDPMCommunication.receivedDataUpdate(from device: PMDevice!)`
	↴
4. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveRowing rowing: EDPMRowing)

## #BT-COMM-5 `communication(_ communication: EDBluetoothCommunicating, didReceiveFixedSplit split: EDPMFixedSplitInterval)`
The `communication(_:didReceiveFixedSplit:)` method is called when a fixed split interval is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by calculating the finished split interval and updating the workout type if the workout is an interval workout that is terminated before reaching the first interval.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `split`: `EDPMFixedSplitInterval` - the fixed split interval received from the PM device

### Details
1.  Check if the calibration is in progress. If so, it returns without doing anything else.
2.  Calculate the finished split interval using `tableWorker` and update the stroke count.
3.  If the workout is an interval workout and is terminated before reaching the first interval, transform the workout into a `justRowSplits` workout.
4.  Add a breadcrumb to the workout analytics.

### Paths

#### 1. Split Update
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `splitIntervalData` - `CE060037-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.splitUpdate`
	↴
3. `PMBLEConnection.saveSplitIntervalForDeviceWithSerialNumber`
	↴
4. `EDPMCommunication.receivedFixedSplit(from device: PMDevice!, fixedSplit: PMSplit!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveFixedSplit split: EDPMFixedSplitInterval)`

#### 2. Extra Split Update
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `extraSplitIntervalData` - `CE060038-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.extraSplitUpdate`
	↴
3. `PMBLEConnection.saveSplitIntervalForDeviceWithSerialNumber`
	↴
4. `EDPMCommunication.**receivedFixedSplit**(from device: PMDevice!, fixedSplit: PMSplit!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveFixedSplit split: EDPMFixedSplitInterval)`

## #BT-COMM-6 `communication(_ communication: EDBluetoothCommunicating,  didReceiveFixedInterval interval: EDPMFixedSplitInterval)`
The `communication(_:didReceiveFixedInterval:)` method is called when data is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by calculating the finished split interval and adding a breadcrumb to the workout analytics.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `interval`: `EDPMFixedSplitInterval` - the received fixed split interval data

### Details
1.  Check if the calibration worker is currently calibrating, and return early if it is.
2.  Calculate the finished split interval using `tableWorker.calculateFinishedSplitInterval(with:)`, passing in an `EDWorkoutTablePMSplitInterval` object created from the received `interval`.
3.  Add a breadcrumb to the workout analytics to indicate that a fixed interval was received.

### Path
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `splitIntervalData` - `CE060037-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.splitUpdate`
	↴
3. `PMBLEConnection.saveSplitIntervalForDeviceWithSerialNumber`
	↴
4. `EDPMCommunication.receivedFixedInterval(from pmDevice: PMDevice!, fixedInterval: PMFixedInterval!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating,  didReceiveFixedInterval interval: EDPMFixedSplitInterval)`

## #BT-COMM-7 `communication(_ communication: EDBluetoothCommunicating,didReceiveVariableInterval variable: EDPMVariableInterval)`
The `communication(_:didReceiveVariableInterval:)` method is called when variable interval data is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by calculating the finished split interval with the received data and storing it in the local array.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `variable`: `EDPMVariableInterval` - the variable interval data received from the PM device

### Details
1.  Check if the calibration worker is not currently calibrating.
2.  Calculate the finished split interval with the received data using `tableWorker.calculateFinishedSplitInterval(with:)`.
3.  Store the received variable interval data in the local array by calling `updateBLEVariableInterval(with:)`.
4.  Add a workout breadcrumb to the analytics log using `analytics.addWorkoutBreadcrumb(.workoutVariableIntervalReceived)`.

### Path
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `splitIntervalData` - `CE060037-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.splitUpdate`
	↴
3. `PMBLEConnection.saveSplitIntervalForDeviceWithSerialNumber`
	↴
4. `EDPMCommunication.receivedVariableInterval(from pmDevice: PMDevice!, variableInterval: PMVariableInterval!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveVariableInterval variable: EDPMVariableInterval)`

___

## #BT-COMM-8 `communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutResults results: Result<EDPMWorkoutResults, Error>)`
The `communication(_:didReceiveWorkoutResults:)` method is called when the workout results are received from a Bluetooth device using `EDBluetoothCommunicating` after the workout is stopped.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `results`: `Result<EDPMWorkoutResults, Error>` - the workout results received from the PM device

### Details
1.  If the results are successfully received, call the `handle(workoutResults:)` function passing in the received `results`. The function logs a debug message indicating the type of workout results received and sets the `isWaitingForResultsResponse` flag to false. If `shouldGetResultsFromMemoryLog` is true, it adds a workout breadcrumb indicating that memory log results have been received, logs a workout event indicating success in reading the PM logbook, and updates the workout with the received results from the memory log. Otherwise, it adds a workout breadcrumb indicating that BLE results have been received, logs a workout event indicating success in assembling raw workout data, and stores the results in `bleInterfaceResults`.
2.  Call the `syncOrRetryGettingResults()` function, which determines if the workout results are ready to be synced and saved. If so, it calls the `saveAndSyncWorkout()` function to save and sync the results. Otherwise, it sets the `shouldGetResultsFromMemoryLog` flag to true and stops the workout to retry calling for memory log results.
3.  If there is an error in receiving the results, add a workout breadcrumb with the error message to the analytics, log a workout event, and return.
4.  If the results are completed with Memory Log data, add a workout breadcrumb for receiving Memory Log results to the analytics, log a workout event for reading Memory Log data success, and update the workout with the received `results` by calling the `updateWorkout(with:source:)` function with `source` set to `.memoryLog`.
5.  If the results are not completed with Memory Log data, add a workout breadcrumb for receiving BLE results to the analytics, log a workout event for assembling workout raw data success, and set the `bleInterfaceResults` variable to the received `results`.
6.  If the results are ready to be synced, call the `saveAndSyncWorkout()` function to save and sync the workout.
7.  If the results are not ready to be synced, set the `shouldGetResultsFromMemoryLog` variable to `true`, and call the `stopWorkout()` function to stop the workout and attempt to call for Memory Log results.

### Paths
#### 1. Terminate Workout (so-called *BLE Interface Results Fetch*) - Immediate Response
1. `EDPMCommunication.getWorkoutResults()`
	↴
2. `PMCommInterface.getWorkoutResultsFromDevices:(NSArray *)devArray`
	↴
3. `PMBLEConnection.terminateWorkout : (NSNumber *) devNumber`
	↴
4. `EDPMCommunication.receivedWorkoutResults(from pmDevice: PMDevice!, results workoutResults: PMWorkoutResults!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutResults results: Result<EDPMWorkoutResults, Error>)`

#### 2. Send 'Get Workout Info' Message (so-called *Memory Log Response*)
1. `EDPMCommunication.getWorkoutResults()`
   `[self sendCSafeMessage:getWorkoutInfoMessage toPMWithSerialNumber:devNumber]`
	↴
2. `PMCommInterface.getWorkoutResultsFromDevices:(NSArray *)devArray`
	↴
3. `PMComm.startPMStatusTimer`
	↴
4. `PMCommInterface.statusUpdateTimeOut`
	↴
5. `PMCommInterface.updateGetWorkoutResults`
	↴
6. `PMBLEConnection.getWorkoutInfo : (NSNumber *) devNumber
	↴
7. `EDPMCommunication.receivedWorkoutResults(from pmDevice: PMDevice!, results workoutResults: PMWorkoutResults!)`
	↴
8. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveWorkoutResults results: Result<EDPMWorkoutResults, Error>)`

___
## #BT-COMM-9 `communication(_ communication: EDBluetoothCommunicating, didReceiveStrokeChange rowing: EDPMRowing)`
The `communication(_:didReceiveStrokeChange:)` method is called when a rowing stroke change is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the workout state by calculating the graph, table, and force plot using the `graphWorker`, `tableWorker`, and `forceCurveWorker` objects respectively.

### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `rowing`: `EDPMRowing` - the rowing data received from the Bluetooth device

### Details
1.  Check if the calibration worker is calibrating. If so, return immediately.
2.  Perform the following operations on the main thread asynchronously:
    1.  Check if the `graphWorker` has a delegate, and if so, call `calculateGraph(with:)` using the rowing data.
    2.  Check if the `tableWorker` has a delegate, and if so, call `calculateTable(with:)` using the rowing data.
    3.  Check if the `forceCurveWorker` has a delegate, and if so, call `calculateForcePlot(with:)` using the rowing data.
    4.  Create an `EDPMIntervalType` object from the `rowingStatus.intervalType` property of the rowing data.
    5.  If the `intervalType` is not a rest interval, create a new `stroke` using the `workoutSaveStrokeUseCase`, and append it to the `workout`.

### Path
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `extraStrokeData` - `CE060036-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
3. `EDPMCommunication.receivedStrokeCountChange(from device: PMDevice!)`
	↴
4. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveStrokeChange rowing: EDPMRowing)`


## #BT-COMM-10 ❌ `communication(_ communication: EDBluetoothCommunicating, didReceiveForceCurvePlot plot: [Int])`
The `communication(_:didReceiveForceCurvePlot:)` method is called when a force curve plot is received from a Bluetooth device using `EDBluetoothCommunicating`. This method updates the force curve worker's current force plot with the received force curve plot.

❌ Disabled according to #74626

#### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `plot`: `[Int]` - the received force curve plot

#### Details
1.  Check if the force curve worker's delegate is not nil.
2.  Update the force curve worker's current force plot with the received force curve plot.

### Path
1. `PMBLEInterface.peripheral:(CBPeripheral *)peripheral didUpdateValueForCharacteristic:(CBCharacteristic *)characteristic error:(NSError *)error`
   Characteristic ID: `forceCurveData` - `CE06003D-43E5-11E4-916C-0800200C9A66`
	↴
2. `PMBLEInterface.parseForceCurveInfo:(NSData *) data forPeripheral:(CBPeripheral *) peripheral`
   Characteristic ID: `extraStrokeData` - `CE060036-43E5-11E4-916C-0800200C9A66`
	↴
3. `PMBLEConnection.rowingStatusUpdate:(NSDictionary *) rowingStatusDict`
	↴
4. `EDPMCommunication.receivedForceCurve(from device: PMDevice!)`
	↴
5. `EDWorkoutInteractor.communication(_ communication: EDBluetoothCommunicating, didReceiveForceCurvePlot plot: [Int])`

## #BT-COMM-11 `communication(_ communication: EDBluetoothCommunicating, didFail error: EDPMCommunicationError)`
The `communication(_:didFail:)` method is called when there is a communication error with a Bluetooth device using `EDBluetoothCommunicating`. This method logs a breadcrumb in the analytics system to record the error.

#### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `error`: `EDPMCommunicationError` - the communication error that occurred

#### Details
1.  Add a breadcrumb to the analytics system to record the communication error.

## #BT-COMM-12 `communication(_ communication: EDBluetoothCommunicating, didReceiveMessage message: [Int], error: Int)`
The `communication(_:didReceiveMessage:error:)` method is called when a message is received from a Bluetooth device using `EDBluetoothCommunicating`. This method logs a breadcrumb in the analytics system to record the received message and any associated error.

#### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `message`: `[Int]` - the received message
-   `error`: `Int` - any associated error with the received message

#### Details
1.  Add a breadcrumb to the analytics system to record the received message and any associated error.

## #BT-COMM-13 `communication(_ communication: EDBluetoothCommunicating, didSend message: [Int])`
The `communication(_:didSend:)` method is called when a message is sent to a Bluetooth device using `EDBluetoothCommunicating`. This method logs a breadcrumb in the analytics system to record the sent message.

#### Arguments
-   `communication`: `EDBluetoothCommunicating` - the object responsible for Bluetooth communication
-   `message`: `[Int]` - the sent message

#### Details
1.  Add a breadcrumb to the analytics system to record the sent message.