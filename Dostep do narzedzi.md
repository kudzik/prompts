# AUDIT-ENV-001 — Inwentaryzacja środowiska, narzędzi i uprawnień agenta

## Rola i cel

Jesteś administratorem środowiska deweloperskiego, specjalistą DevOps, Cloudflare, GitHub i narzędzi agentowych AI.

Przeprowadź szczegółową, **niemutującą inwentaryzację faktycznych możliwości środowiska**, w którym pracujesz nad repozytorium `kudzik/Przepisy` i aplikacją `kucharska.app`.

Wynik zostanie przekazany niezależnemu audytorowi głównemu ChatGPT. Na tej podstawie powstanie protokół współpracy, który umożliwi audytorowi zlecanie ci weryfikacji, testów, diagnostyki oraz późniejszych kontrolowanych prac wdrożeniowych.

Nie ograniczaj odpowiedzi do narzędzi wymienionych poniżej. Samodzielnie wykryj pozostałe dostępne możliwości.

**Bezwzględne zasady:** nie modyfikuj kodu, konfiguracji, baz danych, plików, statusów Issue ani zasobów chmurowych. Nie wykonuj płatnych wywołań modeli. Nie ujawniaj sekretów, tokenów, haseł ani zawartości plików `.env`. Nie wykonuj poleceń publikacyjnych ani destrukcyjnych.

## A. Środowisko wykonawcze

Ustal i udokumentuj:

1. System operacyjny oraz faktyczne środowisko uruchomieniowe (macOS, Windows, WSL, kontener, SSH, inne).
2. Czy pracujesz w VS Code, Google Antigravity, terminalu lokalnym, terminalu zdalnym lub ich kombinacji?
3. Jakie masz możliwości wykonywania poleceń powłoki i skryptów?
4. Czy możesz uruchamiać procesy, serwery lokalne i testy E2E?
5. Czy masz dostęp do internetu oraz lokalnych i zdalnych API?
6. Czy istnieją mechanizmy izolacji, sandboxingu lub ograniczenia uprawnień?
7. Czy możesz bezpiecznie uruchomić testy równolegle?
8. Jak działają limity czasu, zakończenia procesów oraz pobieranie wyników długotrwałych poleceń? Czy potrafisz samodzielnie sprawdzić kod zakończenia procesu?

Przedstaw zainstalowane wersje Node.js, npm, Python, Git, GitHub CLI, Wrangler i Playwright, o ile są dostępne.

## B. Cloudflare — najważniejsza część

Sprawdź faktyczne możliwości Cloudflare Wrangler CLI.

Odpowiedz:

1. Czy `wrangler` jest zainstalowany i działa?
2. Czy jesteś uwierzytelniony? Sprawdź to bez wyświetlania danych uwierzytelniających.
3. Do jakich kont i środowisk masz dostęp? Podaj tylko bezpieczne identyfikatory organizacyjne/środowiskowe.
4. Jakie bazy D1 projektu są dostępne lokalnie, zdalnie, na stagingu i produkcji?
5. Czy możesz wykonywać niemutujące `SELECT` na produkcyjnej D1 przez Wrangler?
6. Czy możesz odczytać strukturę tabel, migracje, schematy i indeksy?
7. Czy możesz odczytać `agent_configs`, `agent_runs`, `recipes`, `pipeline_state_json`, `recipe_media` i `recipe_qa_audits`?
8. Czy masz możliwość wykonywania zapytań przeciw lokalnej kopii D1 lub osobnej bazie testowej?
9. Czy możesz przygotować bezpieczny, zanonimizowany eksport danych diagnostycznych bez ingerencji w produkcję?
10. Czy masz uprawnienia do odczytu obiektów R2 oraz ich metadanych?
11. Czy masz dostęp do logów Cloudflare Workers/Pages, obserwowalności, błędów i trace?
12. Czy istnieje środowisko staging umożliwiające pełne testy integracyjne?
13. Jakie są limity, koszty i ryzyka odczytu produkcyjnych danych?

Wykonaj wyłącznie bezpieczne polecenia diagnostyczne, które nie zmieniają stanu infrastruktury.

Nie wykonuj resetowania bazy, seedowania, migracji, uploadu ani operacji DELETE/UPDATE/INSERT.

## C. GitHub

Sprawdź:

1. Czy `gh auth status` potwierdza uwierzytelnienie?
2. Czy możesz czytać prywatne repozytorium `kudzik/Przepisy`?
3. Czy masz dostęp do GitHub Issues i Project 2?
4. Czy możesz odczytywać PR, komentarze, historię commitów i workflow GitHub Actions?
5. Czy możesz pobierać artefakty testowe i raporty CI?
6. Czy możesz tworzyć lokalne branche, commity oraz uruchamiać testy?
7. Jakie działania GitHub wymagają dodatkowego zatwierdzenia?
8. Czy istnieją ustawienia ochrony gałęzi i polityki merge?

Nie wykonuj `git push`, nie zmieniaj Issues ani Project podczas diagnozy.

## D. Narzędzia testowe

Sprawdź rzeczywistą dostępność:

- Node Test Runner, Vitest lub innych runnerów w projekcie.
- Playwright oraz zainstalowanych przeglądarek.
- Astro build/check.
- Walidatorów JSON Schema, AJV i Zod.
- Testów API oraz integracyjnych.
- Lokalnego Cloudflare Workers/Pages runtime.
- Testowej D1/R2.
- Testów generowania i eksportu Markdown.
- Testów dostępności, np. axe-core.
- Testów wydajności oraz bezpieczeństwa.
- Pokrycia kodu i mutation testing, jeśli dostępne.

Dla każdej kategorii podaj: dostępność, sposób uruchomienia, wymagania środowiskowe i ograniczenia.

## E. Integracje AI i modele

Ustal:

1. Jakie integracje LLM istnieją: OpenRouter, OpenAI, Google, FLUX i pozostałe?
2. Czy możesz odczytać konfiguracje modeli bez ujawniania kluczy?
3. Czy istnieje lokalny mock modeli lub deterministyczny zestaw fixtures?
4. Czy można odtwarzać historyczne odpowiedzi modeli?
5. Czy logi przechowują prompt, odpowiedź, wersję modelu, koszt, czas i identyfikator przebiegu?
6. Czy można testować walidatory i orkiestrację bez płatnych wywołań?
7. Jakie testy koniecznie wymagają rzeczywistych wywołań modeli?

Nie wykonuj żadnego płatnego zapytania.

## F. Komunikacja z audytorem ChatGPT

To kluczowa część diagnozy.

Ustal, jakie masz rzeczywiste możliwości przekazywania dowodów do ChatGPT:

1. Czy możesz zapisywać raporty JSON, Markdown, JUnit XML, Playwright traces lub inne artefakty?
2. Czy możesz udostępniać je poprzez prywatne repozytorium GitHub albo wklejony wynik terminala?
3. Czy możesz przygotowywać kompletne raporty wykonania z kodem zakończenia, SHA commita i informacją o środowisku?
4. Czy możesz wykonywać zestaw poleceń przekazanych przez ChatGPT i zwracać wyniki każdego kroku?
5. Czy możesz uruchamiać ponownie testy wskazane przez audytora i porównywać rezultaty?
6. Czy istnieje dostępny kanał MCP/API, który umożliwiałby ChatGPT bezpośredni odczyt wyników z twojego środowiska?
7. Jakie ograniczenia uniemożliwiają bezpośrednie korzystanie z twoich lokalnych narzędzi przez zewnętrznego audytora?

Nie zakładaj istnienia połączenia ChatGPT z lokalnym terminalem. Oddziel możliwości realnie dostępne od hipotetycznych integracji.

## G. Wymagany raport końcowy

Przygotuj raport z następującymi sekcjami:

1. **Executive Summary** — faktyczne możliwości agenta.
2. **Tool Inventory** — narzędzie, wersja, dostępność i ograniczenia.
3. **Access Matrix** — środowisko, zasób, uprawnienia READ/WRITE, weryfikacja.
4. **Cloudflare Access Report** — rzeczywisty dostęp do D1, R2, Workers i Pages.
5. **Testing Capabilities** — możliwe scenariusze testowe.
6. **Evidence Transfer** — jak przekazać audytorowi niezależnie weryfikowalne wyniki.
7. **Security Boundaries** — czego nie możesz lub nie wolno ci wykonywać.
8. **Recommended Audit Workflow** — proponowana metoda współpracy ChatGPT ↔ Antigravity.
9. **Blockers & Missing Permissions** — faktyczne ograniczenia.
10. **Self-Check** — sprawdzenie kompletności i zgodności odpowiedzi z wynikami diagnostyki.

Każda deklaracja możliwości musi posiadać status:

- `VERIFIED` — sprawdzone bezpiecznym poleceniem lub rzeczywistym użyciem narzędzia;
- `CONFIGURED_NOT_TESTED` — narzędzie skonfigurowane, lecz możliwości jeszcze nie przetestowano;
- `UNAVAILABLE` — niedostępne;
- `UNKNOWN` — brak wystarczających dowodów.

Dla statusu VERIFIED podaj użyte polecenie, wynik w bezpiecznej formie i kod zakończenia.

**Zakończ raport jednoznaczną odpowiedzią:**

„Czy mogę jako agent Antigravity wykonać pełny audyt produkcyjnego Recipe OS na zlecenie ChatGPT, jakie dokładnie dane mogę dostarczyć i jakich uprawnień brakuje?”

Nie rozpoczynaj wdrażania poprawek. Nie zamykaj Issue #42. Wszystkie wyniki przedstaw po polsku.
