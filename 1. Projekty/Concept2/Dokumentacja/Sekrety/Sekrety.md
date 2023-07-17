[[2023-04-23]]
Trafi do `Wiki` projektowego w Azure DevOps.

#### Wersja 🇵🇱
Sekrety to dane poufne takie jak klucze API, adresy URL serwerów, identyfikatory bundle w postaci `klucz:wartość`.

Są to pliki z rozszerzeniem `xcconfig`, które powinny docelowo znaleźć się w katalogu `/ErgData/App/ErgData/SupportingFiles/Configuration/`.

Ze względów bezpieczeństwa nie przechowujemy ich w repozytorium, dlatego w pliku `.gitignore` znajdującym się w głównym folderze repozytorium widnieje zapis `*.xcconfig`.

Pliki te powinny znajdować się wyłącznie w komputerach developerów Concept2 i w bezpiecznej bibliotece DevOps, skąd można kopiować je do ww. katalogu docelowego w procesach CI/CD. Pobranie plików z library na komputer nie jest możliwe.

Operacje pobierania i przenoszenia są zdefiniowane w skryptach YAML pipelines.

Przykład `ergdata-ios-pr`:
```yaml
- task: DownloadSecureFile@1
  name: Debug
  displayName: 'Download Debug Configuration File'
  inputs:
    secureFile: '$(CONFIGURATION_DEBUG_FILENAME)'

- script: |
   echo Installing $(Debug.secureFilePath) to project sources...
   mv $(Debug.secureFilePath) ErgData/App/ErgData/SupportingFiles/Configuration/Debug.xcconfig
  displayName: 'Install Debug.xcconfig'
```

## Edycja plików
Zawartość plików może ulec zmianie i należy dbać o to, by zawartość `Library` DevOps była z nimi spójna. 

W tym celu należy:

1. Otworzyć `Devscale - Concept2` > `Pipelines` > `Library` > `Secure Files`.
![[secrets-secure-files.png]]
2. Następnie wybrać wielokropek (jak na obrazku niżej) i opcję `Delete` (`Edit` w przypadku plików w tym formacie nie wchodzi w grę).
![[secrets-file-options.png]]

3. W bibliotece umieścić zmodyfikowany lokalnie plik o tej samej nazwie wybierając `+ Secure File`.
4. Nadać pipelines uprawnienia do pliku wybierając `{filename}` > `Pipeline Permissions`.
![[secrets-library-permissions.png]]

## Dodanie nowego pliku/zmiana nazwy obecnego
W sytuacji modyfikacji nazwy pliku należy zaktualizować skrypt YAML pipeline i/lub zmienne środowiskowe, które wykorzystują m.in. pliki zgromadzone w katalogu `Library` > `Secure Files`.

W tym celu należy:
1. Przejść do  `Devscale - Concept2` > `Pipelines` > `{pipeline_name}`.
2. Wybrać opcję `Edit`.
![[secrets-edit-pipeline.png]]
3. Dodać nową nazwę pliku lub zmodyfikować zawartość zmiennej środowiskowej wskazującej na obecny.
![[secrets-pipeline-new-variable.png]]

#### Przykład
Przykładowa lista zmiennych środowiskowych wygląda następująco:
![[secrets-pipeline-variables.png]]

Plik `ergdata-ios-pr.yml` obsługujący pipeline `hsl-concept2-ergdata-ios-pr`  odwołuje się do `CONFIGURATION_DEBUG_FILENAME`, czyli `Debug.xcconfig` z `Secure Files`:
```yaml
- task: DownloadSecureFile@1
  name: Debug
  displayName: 'Download Debug Configuration File'
  inputs:
    secureFile: '$(CONFIGURATION_DEBUG_FILENAME)'
```