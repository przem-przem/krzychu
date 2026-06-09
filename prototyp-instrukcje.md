# Prototyp homepage — portfolio Krzysztofa Wargenau (dokumentalisty)

## Czym jest to zadanie

Zbuduj **statyczny prototyp homepage** strony portfolio dla dokumentalisty (wideo + audio).
Cel prototypu: ocena layoutu, typografii, rytmu scrolla i tonu strony — **nie** produkcyjny kod.
Docelowo strona powstanie we Framerze, więc kod ma być prosty i jednorazowy.

**Stack:** czysty HTML + CSS + minimalny vanilla JS. Bez frameworków, bez buildów, bez Tailwinda.
Struktura: `index.html`, `styles.css`, `script.js`. Strona ma działać po otwarciu `index.html` w przeglądarce.

**Język strony:** polski, `<html lang="pl">`. Copy podane niżej wklej **dosłownie** — nie parafrazuj, nie tłumacz, nie "ulepszaj". Tam gdzie copy jest oznaczone `[ROBOCZE]`, też wklej je dosłownie (to znacznik dla nas, nie renderuj go na stronie).

---

## Kontekst projektu (przeczytaj zanim zaczniesz)

Krzysztof Wargenau, lat 30, dokumentalista. Robi wideo i audio dla instytucji publicznych, marek i NGO-sów — reportaże, mini-portrety, materiały promocyjne, które opowiadają zamiast reklamować. Jego metoda: najpierw człowiek, dopiero przez niego pokazany event/produkt/idea.

**Rejestr strony:** ciepły, inteligentny, emocjonalnie uważny, profesjonalny ale nie korporacyjny, **dokumentalnie powściągliwy — zero hype'u i buzzwordów**. Strona ma mówić "twoja historia jest warta opowiedzenia", a nie "patrz, jaki jestem zdolny".

**Zasada przewodnia layoutu i ruchu:** *dokument szanuje obserwowane — nie konkuruje z nim ruchem.* Mało animacji, wolne tempo, dużo powietrza. Powściągliwość to cecha charakteru tej strony, nie brak ambicji.

---

## Kierunek wizualny

### Paleta

Świat tej strony to świat fotografii reportażowej i montażowni: papier, atrament, stykówki, timecode.

- `--paper: #F4F4F1` — tło; neutralna, fotograficzna biel (galeria, nie krem)
- `--ink: #181614` — tekst główny, prawie-czerń
- `--ink-soft: #5C5852` — tekst drugorzędny
- `--line: #D9D7D1` — hairlines, separatory
- `--mark: #C2451E` — akcent "kredka montażysty" (china marker, którym zaznacza się kadry na stykówce). **Używaj go skrajnie oszczędnie:** hover linków, podkreślenie aktywnego elementu, jeden detal w hero. Jeśli akcent pojawia się w więcej niż kilku miejscach na całej stronie — to za dużo.
- Hero jest ciemne (wideo/foto pod spodem): tekst na hero `#F4F4F1`, overlay `rgba(12,11,10,0.35)` + gradient dociążający dół.

### Typografia (Google Fonts, koniecznie z polskimi znakami — subset `latin-ext`)

- **Display + dłuższe teksty:** `Newsreader` (optical sizes; nagłówki light/regular, duże stopnie, ciasny leading). Edytorska, "reporterska" szeryfówka.
- **UI / nawigacja / przyciski / nazwy kategorii:** `Archivo` (regular/medium, sentence case lub caps z letter-spacingiem w drobnych labelach).
- **Meta-dane projektów (klient · format · czas):** `IBM Plex Mono`, małe stopnie, uppercase, letter-spacing ~0.08em — stylizowane na **timecode / opis kadru**. To jest podpis wizualny tej strony: dane techniczne wyglądają jak z planu zdjęciowego.

Skala: H1 hero ~clamp(2.4rem, 6vw, 4.8rem); nagłówki sekcji ~clamp(2rem, 4vw, 3.2rem); body 1.05–1.15rem, line-height 1.6–1.7. Maksymalna szerokość bloków tekstu ~38rem.

### Element-sygnatura

**Claim w hero złożony jak napisy z filmu dokumentalnego (lower third):** osadzony w dolnej-lewej ćwiartce hero, nad nim krótka linia w `IBM Plex Mono` stylizowana na slate / timecode, np. `00:00:01 · KAŻDA HISTORIA`. Cienka pozioma kreska w kolorze `--mark` (szer. ~64px) oddziela slate od claimu. To jedyne miejsce, gdzie akcent występuje w hero.

### Ruch — twarde zasady

- Claim w hero: pojawia się ~1 s po załadowaniu, prosty fade (0.8 s, ease-out). Bez wjazdów liter, bez staggera.
- Sekcje przy scrollu: subtelny fade + translateY(12px), 0.6 s, **raz**, przez IntersectionObserver. Nic więcej.
- Pętle obrazów w "Dowodzie": startują dopiero gdy wiersz jest w viewporcie.
- **Zakazane:** parallax, zoom-y na hover obrazków powyżej scale(1.02), bouncy easing, animowane gradienty, kursory custom, marquee.
- Respektuj `prefers-reduced-motion: reduce` — wtedy wszystko statyczne, crossfade w hero wyłączony (zostaje pierwszy kadr).
- Widoczny `:focus-visible` na wszystkich interaktywnych elementach (outline w `--mark`).

### Czego NIE robić (anty-wzorce)

Żadnych: gradientowych teł, glassmorphizmu, cieni pod kartami, border-radius > 2px, emoji, ikonek dekoracyjnych, "Lorem ipsum" (całe copy jest niżej), badge'ów "⭐ trusted by", sekcji z logotypami, licznikow statystyk. Strona ma wyglądać jak złożona przez człowieka od składu książek, nie jak landing SaaS-a.

---

## Zdjęcia-placeholdery

Nie mamy jeszcze kadrów z materiałów, więc użyj **https://picsum.photos w wersji grayscale** (czarno-białe zdjęcia dobrze symulują rejestr dokumentalny):

- format: `https://picsum.photos/seed/NAZWA/SZER/WYS?grayscale`
- użyj stałych seedów (np. `seed/hero1`, `seed/hero2`, `seed/hero3`, `seed/bread`, `seed/gala`, `seed/dance`, `seed/portrait`), żeby prototyp wyglądał tak samo przy każdym odświeżeniu
- treść zdjęć będzie losowa — to OK, oceniamy kompozycję, nie kadry. Docelowo podmienimy na prawdziwe stille.
- każde `<img>` z sensownym `alt` (po polsku) i `loading="lazy"` poza hero.

---

## Struktura strony — sekcja po sekcji

### 0. Nawigacja (sticky, minimalna)

- Lewa: `Krzysztof Wargenau` (Archivo, medium).
- Prawa: dwa linki — `Realizacje` (na razie `href="#dowod"`) i `Kontakt` (`href="#kontakt"`).
- Na hero nav jest transparentny z jasnym tekstem; po zjechaniu poniżej hero dostaje tło `--paper`, ciemny tekst i hairline border-bottom. Płynna, krótka tranzycja.

### 1. Hero (100vh)

- **Tło:** symulacja reela — 3 pełnoekranowe kadry (picsum grayscale, seedy `hero1/2/3`, np. 1600×900), crossfade w pętli: każdy kadr widoczny ~4 s, przenikanie ~1.2 s. **Bez zoomu, bez ruchu kamery** — sam crossfade. (Docelowo będzie tu pętla wideo.)
- **Overlay** przyciemniający (mocniejszy przy dolnej krawędzi), żeby tekst był czytelny.
- **Lower third (dolna-lewa ćwiartka):**
  - linia slate (IBM Plex Mono, mała, uppercase): `00:00:01 · KAŻDA HISTORIA`
  - kreska 64px w `--mark`
  - **H1 (Newsreader):** `Każda historia ma ludzki wymiar. Opowiedzmy Twoją.` — złamane na dwie linie dokładnie po kropce.
  - **Subline (Archivo, mniejszy stopień, jaśniejszy):** `Dokumentalne wideo i audio dla instytucji, marek i organizacji.`
- Dyskretna wskazówka scrolla na dole środka: sama pionowa kreska 1×32px, delikatnie pulsująca opacity (to jedyny zapętlony ruch poza crossfade).
- Mobile: zamiast crossfade'u **jeden statyczny pionowy kadr** (np. `seed/hero-mobile`, 900×1400), lower third zostaje.

### 2. Orientacja

Jasne tło (`--paper`), dużo powietrza (padding pionowy min. 8rem na desktopie). Bez nagłówka sekcji — sekcję otwiera od razu statement.

**Statement (Newsreader, duży stopień, max ~20 słów na linię):**

> Jestem dokumentalistą. Robię wideo i audio o ludziach, którzy stoją za działaniami organizacji — reportaże, mini-portrety, materiały, które opowiadają zamiast reklamować.

**Pod statementem: trzy wiersze kategorii** (pełna szerokość kontenera, oddzielone hairlinami `--line`, generous padding pionowy). Każdy wiersz: nazwa kategorii (Archivo, medium) + jedno zdanie (Newsreader lub Archivo regular, `--ink-soft`). Wiersze są **statyczne** — bez linków, bez strzałek. Na hover delikatne podbicie koloru nazwy do `--mark` (zapowiedź przyszłej interakcji, nic więcej).

> **Instytucjom publicznym** — pomagam pokazać, że za ich projektami stoją ludzie i sens, zanim utonie to w komunikatach.
>
> **Markom, które wolą opowiadać niż reklamować** — robię materiały o wartościach i ludziach, nie o „ofercie".
>
> **NGO-som i kampaniom społecznym** — daję formę, która niesie temat dalej niż raport z projektu.

### 3. Dowód — wybrane realizacje (`id="dowod"`)

**Nagłówek sekcji (Newsreader):** `Historie, które już opowiedziałem`

**To NIE jest grid kart.** Trzy **pełnoszerokościowe wiersze edytorskie**, naprzemiennie: obraz po lewej / treść po prawej, potem odwrotnie. Obraz zajmuje ~55–60% szerokości, proporcje 16:10. Duże odstępy pionowe między wierszami (min. 7rem) — sekcja ma się scrollować wolno i spokojnie.

Anatomia wiersza:
- **obraz** (picsum grayscale; symuluje ruchomy kadr — wystarczy statyczny, ale dodaj na nim w rogu mały znacznik `▸ 0:05` w IBM Plex Mono, sugerujący pętlę),
- **linia meta** (IBM Plex Mono, uppercase, mała, `--ink-soft`),
- **nagłówek historii** (Newsreader, ~2rem),
- **hook** (1 zdanie, body),
- **link `Zobacz historię →`** (Archivo; podkreślenie w `--mark` na hover; `href="#"` — strony projektów to osobny etap).

Treści trzech wierszy, w tej kolejności:

**Wiersz 1 — obraz seed/bread**
- meta: `MADAME BREAD · REKLAMA DOKUMENTALNA · 05:00`
- nagłówek `[ROBOCZE]`: `Piekarnia, w której najważniejsi są ludzie`
- hook `[ROBOCZE]`: `Opowieść o rzemiośle i codzienności piekarni — bez słowa o ofercie, za to z ludźmi, którzy wstają przed świtem.`

**Wiersz 2 — obraz seed/gala**
- meta: `NARODOWY INSTYTUT MUZYKI I TAŃCA · REPORTAŻ · 12:00`
- nagłówek `[ROBOCZE]`: `Pięćdziesiąta gala, pół wieku sztuki ludowej`
- hook `[ROBOCZE]`: `Reportaż z gali 50. Nagrody im. Oskara Kolberga na Zamku Królewskim — o twórcach, którzy rzadko stoją w świetle reflektorów.`

**Wiersz 3 — obraz seed/dance**
- meta: `NARODOWY INSTYTUT MUZYKI I TAŃCA · SYLWETKA · 01:00`
- nagłówek `[ROBOCZE]`: `Tancerka w przeddzień światowego konkursu`
- hook `[ROBOCZE]`: `Krótki portret Anny Hop przed międzynarodowym konkursem tanecznym — energia sceny zamknięta w jednej minucie.`

Pod trzecim wierszem, wyśrodkowany, link: `Zobacz wszystkie realizacje →` (`href="#"`, ten sam styl co linki wierszy, większy stopień).

### 4. Kim jestem — `[SEKCJA LOW-FI — jeszcze nieprojektowana, zbuduj prosto]`

Dwukolumnowo: lewa — pionowy portret (picsum `seed/portrait`, 800×1000, grayscale); prawa — tekst.

- **Nagłówek `[ROBOCZE]`:** `Kim jestem`
- **Bio `[ROBOCZE]`, 2 akapity:**

> Skończyłem dokumentalistykę i od kilku lat robię materiały, w których kamera i mikrofon służą temu samemu: zrozumieniu człowieka po drugiej stronie. Pracuję blisko ludzi, bez scenariusza wciskanego im w usta — to, co mówią, jest ich, nie moje.
>
> Wierzę, że dobrze opowiedziana historia nie potrzebuje fajerwerków. Potrzebuje uwagi, czasu i kogoś, kto wie, kiedy nie przeszkadzać.

- **Workflow — 4 kroki** (tu numeracja `01–04` w IBM Plex Mono jest uzasadniona, bo to realna sekwencja; każdy krok: numer, nazwa w Archivo medium, jedno zdanie):

> `01 Rozmowa` — poznaję organizację, ludzi i to, co naprawdę chcecie powiedzieć.
> `02 Oś opowieści` — ustalamy, czyją historią to opowiemy i w jakiej formie.
> `03 Nagrania` — dokumentuję, nie reżyseruję; ludzie mają czas być sobą.
> `04 Montaż` — historia dostaje rytm, oddech i długość, jakiej potrzebuje.

### 5. Kontakt (`id="kontakt"`) — `[SEKCJA LOW-FI — jeszcze nieprojektowana, zbuduj prosto]`

Wąska kolumna, wycentrowana.

- **Nagłówek (Newsreader) `[ROBOCZE]`:** `Opowiedzmy Twoją historię.` *(domyka claim z hero)*
- **Zdanie pod nagłówkiem `[ROBOCZE]`:** `Napisz kilka słów o swojej organizacji i o tym, co chcesz pokazać — odezwę się, żeby porozmawiać.`
- **Formularz:** `Imię` (text) · `E-mail` (email) · `O czym jest Twoja historia?` (textarea, 5 wierszy) · przycisk `Wyślij` (Archivo; tło `--ink`, tekst `--paper`; hover: tło `--mark`).
- Bez backendu: na submit `preventDefault()` i podmiana formularza na tekst: `Dziękuję. Odezwę się w ciągu kilku dni.`
- Pod formularzem, drobnym: `Wolisz maila? kontakt@przyklad.pl` (placeholder).

### 6. Stopka

Hairline u góry. Jedna linia: `Krzysztof Wargenau · dokumentalista` po lewej, `© 2026` po prawej. IBM Plex Mono, małe, `--ink-soft`. Nic więcej.

---

## Responsywność

- Breakpointy: ~1200 / ~768 / ~420 px.
- Mobile: hero ze statycznym pionowym kadrem; wiersze "Dowodu" stackują się (obraz nad treścią); "Kim jestem" stackuje (portret nad tekstem); nav bez zmian (dwa linki się mieszczą).
- Typografia przez `clamp()`, padding sekcji skaluje się w dół (~4rem na mobile).

## Kryteria ukończenia

1. `index.html` otwiera się z dysku i wszystko działa (crossfade hero, fade-in sekcji, pętla startująca w viewporcie — tu wystarczy znacznik, formularz z podmianą).
2. Całe copy wklejone dosłownie, polskie znaki renderują się poprawnie.
3. `prefers-reduced-motion` i `:focus-visible` obsłużone.
4. Zero elementów z listy anty-wzorców.
5. Na końcu wypisz krótko (w 3–4 punktach), jakie decyzje wizualne podjąłeś tam, gdzie spec zostawiał luz — to materiał do review.
