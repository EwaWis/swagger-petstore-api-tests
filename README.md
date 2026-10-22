# Automatyzacja Testów w CI/CD: Praktyczne Warsztaty z Jenkins i GitHub Actions

Cześć!

To repozytorium to projekt, na którym będziemy pracować podczas ostatnich warsztatów z naszej serii o automatyzacji testów: testy API dla [Swagger Petstore](https://petstore.swagger.io/) napisane w Playwright i TypeScript.

Zanim przyjdziesz na warsztat, przygotuj środowisko zgodnie z sekcją **INSTRUKCJE DO WARSZTATU**.

## Przydatne Linki

- Notatki: https://docs.google.com/document/d/1B28pDWSgCERwUmVSBAydnlIFZJ4CnRoYswfFAW0YeFY/edit?usp=sharing
- Zadania i Rozwiązania: https://drive.google.com/drive/folders/1gS1ln2tKxObkRsWSSgpCUoWRsFx5B7g6?usp=sharing

## INSTRUKCJE DO WARSZTATU

Przyjdź na warsztat z **laptopem** – najlepiej z systemem **Windows**.
Upewnij się, że na laptopie nie masz ograniczeń, takich jak:

- brak uprawnień do instalowania narzędzi,
- blokady dostępu do sieci (firmowy VPN, polityki bezpieczeństwa, proxy itp.).

## Wymagania wstępne

### Umiejętności
- Podstawowa znajomość testowania oprogramowania i systemu kontroli wersji
- Konto GitHub oraz podstawowa wiedza o Git

### Wymagania techniczne

#### 1. Zainstaluj Visual Studio Code
Pobierz i zainstaluj z:
[https://code.visualstudio.com/download](https://code.visualstudio.com/download)

#### 2. Zainstaluj Java JDK (wersja 17 lub nowsza)
Java jest potrzebna do uruchomienia lokalnego agenta Jenkins podczas warsztatu.
Pobierz z:
[https://www.oracle.com/java/technologies/downloads/](https://www.oracle.com/java/technologies/downloads/)

Po instalacji sprawdź w terminalu:
```bash
java -version
javac -version
```

Obie komendy powinny zwrócić zainstalowaną wersję JDK.

#### 3. Zainstaluj Node.js (wersja LTS)
Node.js i npm będą wykorzystywane do instalowania zależności oraz uruchamiania testów Playwright.
Pobierz z:
[https://nodejs.org/](https://nodejs.org/)

Następnie sprawdź instalację:
```bash
node --version
npm --version
```

#### 4. Zainstaluj Git, jeśli nie jest jeszcze zainstalowany
Pobierz z:
[https://git-scm.com/downloads](https://git-scm.com/downloads)

```bash
git --version
```

## GitHub i konfiguracja projektu

#### 5. Forkuj repozytorium
Przejdź do:
https://github.com/tklepacki/swagger-petstore-api-tests

Kliknij **Fork**, aby utworzyć kopię na swoim koncie GitHub.

Nie masz konta na GitHubie? Najpierw utwórz je na [https://github.com](https://github.com)

#### 6. Sklonuj swoje sforkowane repozytorium
```bash
git clone https://github.com/TWOJ_USERNAME/swagger-petstore-api-tests.git
```

#### 7. Otwórz projekt w VS Code
Przejdź do sklonowanego folderu i otwórz go w VS Code.

#### 8. Zainstaluj zależności projektu
```bash
npm ci
```

#### 9. Sprawdź, czy testy API uruchamiają się lokalnie
```bash
npx playwright test
```

Wszystkie testy (42) powinny zakończyć się sukcesem. Raport HTML otworzysz poleceniem:
```bash
npx playwright show-report
```

W projekcie API nie instalujemy przeglądarek Playwright – polecenie `npx playwright install` nie jest potrzebne.

## Docker i Jenkins

#### 10. Zainstaluj Docker Desktop
Pobierz z:
[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

Po instalacji sprawdź wersję:
```bash
docker -v
```

#### 11. Pobierz obraz Dockera z Jenkinsem
```bash
docker pull jenkins/jenkins:lts
```

## Wszystko gotowe!

Upewnij się, że wszystko jest zainstalowane i działa **przed warsztatem**. W razie problemów napisz do mnie.

Do zobaczenia! :)

---

## O projekcie

Testy API zasobu `/pet` w [Swagger Petstore](https://petstore.swagger.io/), napisane w Playwright i TypeScript, ze schematami odpowiedzi w Zod.

```
tests/
├── api/pet/
│   ├── create-pet.spec.ts       # POST /pet
│   ├── get-pet.spec.ts          # GET /pet/{id}
│   ├── update-pet.spec.ts       # PUT /pet, POST /pet/{id}
│   ├── delete-pet.spec.ts       # DELETE /pet/{id}
│   ├── find-by-status.spec.ts   # GET /pet/findByStatus
│   └── upload-image.spec.ts     # POST /pet/{id}/uploadImage
├── fixtures/
│   └── api.fixture.ts           # fixture withPet z automatycznym sprzątaniem
├── factories/
│   └── pet.factory.ts           # fabryka danych testowych
├── helpers/
│   └── pet-client.ts            # klient HTTP
└── schemas/
    └── pet.schema.ts            # schematy Zod
```

| Polecenie | Co robi |
|---|---|
| `npm test` | wszystkie testy |
| `npm run test:smoke` | tylko testy `@smoke` |
| `npm run test:regression` | tylko testy `@regression` |
| `npm run report` | otwiera raport HTML |

Domyślnie testy uderzają w `https://petstore.swagger.io/v2/`.
