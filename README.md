# Robot

Proces, który będziemy budować to `Consumer` aplikacji UiDemo. Nasza automatyzacja będzie pobierała wartości `Cash In`, `On Us Check` i `Not On Us Check` z kolejki Orchestratora i wpisywała je do aplikacji UiDemo. Kolejka zostanie wypełniona poprzez Upload Items w Orchestratorze, aby dodać wszystkie wiersze z pliku CSV jako transakcje w kolejce.


Zgodnie z najlepszą praktyką dla każdego procesu, który automatyzujesz, przed rozpoczęciem konfiguracji frameworków, poszukaj części procesu, które mogą być ponownie wykorzystane. Jest to bardzo pomocne przy dzieleniu się kodem, a nawet ponownym wykorzystaniu fragmentów w ramach tego samego projektu.
