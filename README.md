# KsefSyncer-releases

Repozytorium **wydań** aplikacji KsefSyncer (do wersji 0.9.2: KsefSender) – wysyłka faktur z Comarch ERP XL do KSeF 2.0. Zawiera wyłącznie
paczki i notatki wydań; kod źródłowy jest w osobnym repozytorium. Z tego repozytorium serwery pobierają nowe wersje poleceniem
`KsefSyncer.exe update` (na serwerach zainstalowanych do wersji 0.9.2 plik nadal nazywa się `KsefSender.exe` – aktualizacja nie zmienia nazwy pliku).

## Konwencja

- Tag `v<wersja>` (np. `v0.9.3`) równy wersji aplikacji (`--version`).
- Zasoby wydania (od 0.9.3):
  - `KsefSyncer-<wersja>.zip` (paczka: `KsefSyncer.exe`, `appsettings.json`, `appsettings.local.example.json`, `schemas\`, `db\`)
    oraz `KsefSyncer-<wersja>.zip.sha256` (suma SHA-256 paczki w formacie `sha256sum`);
  - **paczka zgodności** `KsefSender-<wersja>.zip` i `KsefSender-<wersja>.zip.sha256` – ta sama zawartość z plikiem exe pod starą nazwą
    `KsefSender.exe`; pobiera ją `update` w wersji 0.9.2, które zna tylko starą konwencję nazw. Publikowana, dopóki którykolwiek serwer ma 0.9.2.
  - Wydanie `v0.9.2` ma tylko `KsefSender-0.9.2.zip` i `.sha256` (stara konwencja); nowsze wersje umieją je pobrać (`update --to 0.9.2`).
- Treść wydania to notatki: co nowego i czy wersja wymaga migracji schematu rejestru (wtedy pierwsza linia zaczyna się od
  "Wymaga migracji schematu rejestru").
- Wydania oznaczone jako pre-release instalują tylko serwery z `Update.AllowPrerelease = true` (serwer testowy).
- Wydań się nie kasuje: `update --to <wersja>` pozwala wrócić do każdej opublikowanej wersji.

Wydania tworzy workflow `release.yml` w repozytorium z kodem (po wypchnięciu tagu `v<wersja>`) albo ręcznie `gh release create`.
Repozytorium jest **publiczne** (decyzja właściciela 2026-09-24): serwery nie potrzebują żadnego tokena, a paczka nie zawiera sekretów.
Kod źródłowy aplikacji pozostaje w prywatnym repozytorium. Gdyby to repozytorium kiedyś stało się prywatne, serwery potrzebowałyby
`Update.Token` (fine-grained PAT z prawem *Contents: read* wyłącznie do tego repozytorium) w `appsettings.local.json`.
