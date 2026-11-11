# Polityka bezpieczeństwa

## Zgłaszanie podatności

Nie zgłaszaj podatności w publicznym issue. Użyj prywatnego zgłoszenia:
**Security → Report a vulnerability** w tym repozytorium (GitHub Private Vulnerability Reporting).

Odpowiedź przyjdzie w ciągu 7 dni.

## Zasady dotyczące sekretów

1. **Żadnych sekretów w kodzie.** Klucze API, tokeny, hasła i adresy prywatnych usług nigdy nie trafiają do repozytorium, nawet na chwilę i nawet w gałęzi roboczej. Historia gita jest publiczna i trwała.
2. **Zmienne środowiskowe.** Lokalne sekrety trzymaj w pliku `.env`, który jest ignorowany przez git. Wzór, bez wartości, jest w `.env.example`.
3. **CI/CD.** Sekrety dla GitHub Actions dodawaj tylko w *Settings → Secrets and variables → Actions* i odwołuj się do nich przez `${{ secrets.NAZWA }}`.
4. **Wyciek.** Jeśli sekret trafi do repozytorium, natychmiast go unieważnij i wygeneruj nowy u dostawcy. Samo usunięcie pliku nie wystarczy, bo sekret zostaje w historii.

## Zabezpieczenia w repozytorium

| Warstwa | Narzędzie |
|---|---|
| Wykrywanie sekretów przy pushu | GitHub Secret Scanning + Push Protection |
| Wykrywanie sekretów w CI (cała historia) | Gitleaks (`.github/workflows/security.yml`) |
| Wykrywanie sekretów przed commitem | pre-commit + Gitleaks (`.pre-commit-config.yaml`) |
| Analiza statyczna kodu | CodeQL (`.github/workflows/codeql.yml`) |
| Aktualizacje zależności CI | Dependabot (`.github/dependabot.yml`) |
| Łańcuch dostaw | Akcje przypięte do SHA commitów, minimalne uprawnienia `GITHUB_TOKEN` |
| Przeglądarka | Content Security Policy, `referrer: no-referrer`, escapowanie tekstu wpisanego przez użytkownika |

## Konfiguracja lokalna

```bash
pip install pre-commit
pre-commit install   # od teraz każdy commit jest skanowany pod kątem sekretów
```
