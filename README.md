# Iskra – trening umysłu

Aplikacja webowa do treningu mózgu i umiejętności miękkich. Ma gry wzorowane na metodach z badań naukowych, quizy z wiedzy ogólnej (ponad 1000 pytań) i animowane scenki rozmów.

## Co jest w środku

- **Gry rozwojowe** wzorowane na metodach z badań: Podwójna decyzja (szybkość przetwarzania, UFOV), Obracanie figur, Pułapki myślenia, kalibracja pewności, Przedział 90%, powtórki w odstępach, Czytanie emocji, Przeformułuj myśl, Nietypowe zastosowania i Licz oddechy.
- **Trening dnia** w trzech długościach: krótki, standardowy i długi.
- **Wiedza**: teleturniej, quizy tematyczne i krótkie lekcje.
- **Rozmowy**: scenki z wyborem odpowiedzi, w tym sekcja „Dusza towarzystwa”.
- **Ćwiczenia** i zręcznościówki na rozgrzewkę.

## Uruchomienie

To jeden plik `index.html` bez zależności i bez procesu budowania.

```bash
# dowolny statyczny serwer, np.:
python3 -m http.server 8000
# a potem otwórz http://localhost:8000
```

## Dane i prywatność

- Postęp zapisuje się lokalnie w przeglądarce (`localStorage`, klucz `iskra-v1`).
- Gdy aplikacja działa jako artefakt w Claude, postęp synchronizuje się też z chmurą platformy przez wbudowane API (`window.claude`). Kod nie zawiera żadnych kluczy, tokenów ani adresów backendu. Uwierzytelnianie zapewnia platforma.
- Aplikacja nie zbiera danych osobowych i nie wysyła ich do zewnętrznych serwisów. Jedyne zewnętrzne zasoby to czcionki z Google Fonts.

## Bezpieczeństwo

Szczegóły są w [SECURITY.md](SECURITY.md). W skrócie:

- **Content Security Policy:** w `index.html` blokuje skrypty, ramki i połączenia z obcych domen.
- **Sekrety:** w repozytorium nie ma żadnych. Gdyby kiedyś były potrzebne, trafiają do zmiennych środowiskowych (`.env`, ignorowany przez git) albo do GitHub Actions Secrets. Wzór jest w `.env.example`.
- **Automatyczne skanowanie:** Gitleaks szuka sekretów w całej historii, a CodeQL analizuje kod przy każdym pushu i pull requeście.
- **Aktualizacje:** Dependabot pilnuje akcji GitHub. Akcje są przypięte do konkretnych commitów.
- **Lokalnie:** hook pre-commit z Gitleaks zatrzymuje commit, w którym jest sekret.
