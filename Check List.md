# REFramework Orchestrator Queues

## Lista kontrolna REF z elementami kolejki

### Wymagania wstępne

- [ ] Robot połączony z Orchestratorem
- [ ] Kolejka utworzona w Orchestratorze
  - [ ] Ustawiona wartość `Retry`
  
### Konfiguracja w UiPath Studio

- [ ] Utwórz nowy projekt używając szablonu Robotic Enterprise Framework
  - [ ] Ustawienie odpowiedniej nazwy dla projektu - na podstawie nazwy zautomatyzowanego procesu
  - [ ] Ustawienie odpowiedniego opisu dla projektu  
- [ ] Edycja pliku konfiguracyjnego projektu, znajdującego się w folderze projektu, `Data/Config.xlsx`
  - [ ] Arkusz ustawień (`Settings sheet`)
    - [ ] Ustawienie prawidłowej wartości parametru `OrchestratorQueueName` Użyj tej samej nazwy, co kolejka utworzona dla tego procesu w Orchestratorze.
    - [ ] Należy ustawić właściwą wartość parametru `OrchstratorQueueFolder`, można pozostawić go pustym, jeśli kolejka znajduje się w tym samym folderze co proces.
    - [ ] Ustawić odpowiednią nazwę dla parametru `logF_BussinessProcessName`. Jest to przydatne, żeby powiązać proces z komunikatami logów generowanymi podczas jego wykonywania.
    - [ ] Zdefiniuj wszelkie dodatkowe parametry wymagane dla procesu, takie jak ścieżki plików wejściowych, ścieżki aplikacji, parametry sterujące przepływem automatyzacji, wiadomości e-mail, itp.
    - [ ] Zasoby poświadczeń (Credential assets) powinny być również zdefiniowane w tym arkuszu, zamiast w arkuszu `Assets sheet`
  - [ ] Arkusz stałych (`Constants sheet`)
    - [ ] Pozostaw wartość MaxRetryNumber na `0`, będziesz używał mechanizmu retry na poziomie kolejki jeśli będzie to konieczne
    - [ ] Opcjonalnie można zmienić wartości innych elementów zdefiniowanych w tym arkuszu w zależności od automatyzowanego procesu.
  - [ ] Arkusz aktywów (`Assets sheet`)
    - [ ] Dodaj wpisy dla wszystkich assetów zdefiniowanych w Orchestratorze dla tego procesu (oprócz assetów poświadczających)
  - [ ] Zapisz i zamknij plik `Config.xlsx`

### Wykorzystywane aplikacji: open/close/kill

- [ ] Edytuj przepływ pracy (workflow) `Framework/InitAllApplications.xaml`, powinien on zawierać działania mające na celu uruchomienie wszystkich aplikacji, przeprowadzenie uwierzytelnienia i wstępnej konfiguracji wymaganej dla wszystkich transakcji w procesie.
- [ ] Edytuj przepływ `Framework/CloseAllApplication.xaml`, wywołaj tutaj aktywności, które powinny wylogować i zamknąć aplikacje otwarte w przepływie `InitAllApplications.xaml`
- [ ] Edytuj przepływ pracy `Framework/KillAllProcesses.xaml`, umieść tu działania wymuszające zamknięcie aplikacji używanych w automacie.

### Proces biznesowy: Dane transakcyjne i proces

- [ ] Edycja przepływu pracy `Framework/GetTransactionData.xaml`
  - [ ] Ustaw odpowiednią wartość dla argumentu `out_TransactionID`, w czynności `Assign out_TransactionID`
  - [ ] Ustaw odpowiednie wartości dla argumentów `out_TransactionField1` i `out_TransactionField2` w dwóch kolejnych zadaniach
- [ ] Edytuj workflow `frameworki/Process.xaml`
  - [ ] Umieść wszystkie działania i logikę wymaganą do przetworzenia jednej transakcji.
