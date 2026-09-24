# KsefSyncer-releases

Repozytorium **wydań** aplikacji KsefSender (wysyłka faktur z Comarch ERP XL do KSeF 2.0). Zawiera wyłącznie paczki i notatki wydań;
kod źródłowy jest w osobnym repozytorium. Z tego repozytorium serwery pobierają nowe wersje poleceniem `KsefSender.exe update`.

## Konwencja

- Tag `v<wersja>` (np. `v0.9.2`) równy wersji aplikacji (`KsefSender.exe --version`).
- Zasoby wydania: `KsefSender-<wersja>.zip` (paczka: `KsefSender.exe`, `appsettings.json`, `appsettings.local.example.json`, `schemas\`, `db\`)
  oraz `KsefSender-<wersja>.zip.sha256` (suma SHA-256 paczki w formacie `sha256sum`).
- Treść wydania to notatki: co nowego i czy wersja wymaga migracji schematu rejestru (wtedy pierwsza linia zaczyna się od
  "Wymaga migracji schematu rejestru").
- Wydania oznaczone jako pre-release instalują tylko serwery z `Update.AllowPrerelease = true` (serwer testowy).
- Wydań się nie kasuje: `KsefSender.exe update --to <wersja>` pozwala wrócić do każdej opublikowanej wersji.

Wydania tworzy workflow `release.yml` w repozytorium z kodem (po wypchnięciu tagu `v<wersja>`) albo ręcznie `gh release create`.
Repozytorium jest **publiczne** (decyzja właściciela 2026-09-24): serwery nie potrzebują żadnego tokena, a paczka nie zawiera sekretów.
Kod źródłowy aplikacji pozostaje w prywatnym repozytorium. Gdyby to repozytorium kiedyś stało się prywatne, serwery potrzebowałyby
`Update.Token` (fine-grained PAT z prawem *Contents: read* wyłącznie do tego repozytorium) w `appsettings.local.json`.
