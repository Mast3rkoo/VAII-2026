# Navarené

Filip Noga

5ZYI31

## Stručný opis projektu

Navarené je webová aplikácia na zdieľanie a vyhľadávanie receptov. Rieši problém rozhádzaných receptov v rôznych zošitoch, poznámkach a na weboch a takisto aj problém zabudnutia niektorého z receptov. Používatelia si recepty môžu uložiť na jedno miesto, zaradiť do kategórií a zdieľať s ostatnými, čím sa vyhnú zabudnutiu alebo strate receptov.

Aplikácia je určená pre každého, kto varí, od začiatočníkov, ktorí hľadajú inšpiráciu, po skúsených kuchárov, ktorí chcú zdieľať vlastné recepty. Hlavným účelom je jednoduché pridávanie receptov, ich vyhľadávanie podľa názvu, kategórie či surovín a hodnotenie receptov komunitou. Recepty takisto môžu obsahovať aj výživové hodnoty, čo je skvelá správa pre ľudí, ktorí si chcú upraviť svoj jedálniček.

## Role v projekte

- **Návštevník (neprihlásený)** - môže prezerať a vyhľadávať recepty a čítať komentáre. Nemôže pridávať obsah.
- **Registrovaný používateľ** - má všetky oprávnenia návštevníka, navyše môže pridávať, upravovať a mazať vlastné recepty, hodnotiť a komentovať recepty ostatných a ukladať si obľúbené recepty.
- **Administrátor** - spravuje celý obsah aplikácie. Môže upravovať a mazať akékoľvek recepty a komentáre, spravovať kategórie a blokovať používateľov.

## Prípady použitia podľa rolí

**Návštevník**

- Návštevník si prezrie zoznam najnovších receptov.
- Návštevník vyhľadá recept podľa názvu alebo suroviny.
- Návštevník filtruje recepty podľa kategórie.
- Návštevník si zobrazí detail receptu.
- Návštevník sa zaregistruje.

**Registrovaný používateľ**

- Používateľ sa prihlási a odhlási.
- Používateľ pridá nový recept.
- Používateľ upraví alebo zmaže svoj recept.
- Používateľ ohodnotí recept (1-5 hviezdičiek).
- Používateľ pridá komentár k receptu.
- Používateľ si uloží recept medzi obľúbené.
- Používateľ si upraví svoj profil.

**Administrátor**

- Administrátor pridá, upraví alebo zmaže kategóriu.
- Administrátor zmaže nevhodný recept alebo komentár.
- Administrátor zablokuje používateľa.

## Plánované entity

- **Používateľ (User)** - registrovaný používateľ systému.
  Atribúty: id, meno, email, heslo (hash), rola (user/admin), dátum registrácie, zablokovaný (true/false).
- **Recept (Recipe)** - samotný recept.
  Atribúty: id, názov, popis, postup, čas prípravy, počet porcií, obrázok, dátum vytvorenia, autor (FK User), kategória (FK Category).
- **Kategória (Category)** - zaradenie receptu, napr. polievky, dezerty, hlavné jedlá.
  Atribúty: id, názov.
- **Surovina (Ingredient)** - surovina, ktorá sa môže použiť vo viacerých receptoch.
  Atribúty: id, názov.
- **Surovina v recepte (RecipeIngredient)** - spojovacia entita medzi receptom a surovinou.
  Atribúty: recept (FK), surovina (FK), množstvo, jednotka.
- **Komentár (Comment)** - komentár používateľa k receptu.
  Atribúty: id, text, dátum, autor (FK User), recept (FK Recipe).
- **Hodnotenie (Rating)** - hodnotenie receptu používateľom.
  Atribúty: id, počet hviezdičiek (1-5), používateľ (FK User), recept (FK Recipe).

## Vzťahy medzi entitami

- **Používateľ- Recept (1:N)** - používateľ môže vytvoriť viac receptov, recept má jedného autora.
- **Kategória – Recept (1:N)** - kategória obsahuje viac receptov, recept patrí do jednej kategórie.
- **Recept – Surovina (M:N)** - recept obsahuje viac surovín a surovina sa nachádza vo viacerých receptoch.
- **Používateľ - Komentár (1:N)** a **Recept - Komentár (1:N)** - používateľ píše komentáre, recept má viac komentárov.
- **Používateľ - Hodnotenie (1:N)** a **Recept - Hodnotenie (1:N)** - jeden používateľ môže daný recept ohodnotiť len raz.
- **Používateľ - Recept (M:N, obľúbené)** - používateľ si môže uložiť viac obľúbených receptov, recept môže byť obľúbený u viacerých používateľov.

## Hlavné stránky aplikácie

1. **Domovská stránka** - zoznam najnovších a najlepšie hodnotených receptov, vyhľadávacie pole.
2. **Zoznam receptov** - všetky recepty s filtrom podľa kategórie a vyhľadávaním, stránkovanie.
3. **Detail receptu** - obrázok, suroviny, postup, priemerné hodnotenie, komentáre, tlačidlo „Pridať do obľúbených“.
4. **Pridanie / úprava receptu** - formulár s validáciou, dynamické pridávanie surovín.
5. **Prihlásenie a registrácia** - formuláre na vytvorenie účtu a prihlásenie.
6. **Môj profil** - údaje používateľa, zoznam jeho receptov a obľúbených receptov.
7. **Administrácia** - správa kategórií, používateľov a nevhodného obsahu.

## Rozdelenie funkcionality

**Základné funkcie**

- Registrácia, prihlásenie, odhlásenie používateľa.
- CRUD operácie s receptami (pridanie, zobrazenie, úprava, zmazanie).
- CRUD operácie s kategóriami (administrátor) a s komentármi (autor / administrátor).
- Priradenie receptu ku kategórii a pridanie surovín.
- Nahrávanie obrázka k receptu - kontrola typu a veľkosti súboru, výmena obrázka pri úprave a zmazanie súboru pri zmazaní receptu.
- Zoznam receptov a detail receptu.
- AJAX: vyhľadávanie a filtrovanie receptov podľa názvu a kategórie bez obnovenia stránky.
- AJAX: pridávanie a mazanie komentárov bez obnovenia stránky.
- AJAX: pridanie / odobranie receptu z obľúbených.
- Rozlíšenie rolí a autorizácia (používateľ smie upravovať len svoje recepty, admin všetko; neprihlásený nemá prístup k chráneným akciám).
- Kontrola všetkých vstupov na strane klienta (JavaScript) aj servera (PHP), ochrana proti SQL injection a XSS.
- Responzívny dizajn (mobil, tablet, desktop).
- Spustenie v Dockeri s automatickým importom ukážkových dát (používatelia, kategórie, recepty).

**Rozširujúce funkcie**

- Hodnotenie receptov hviezdičkami a zoradenie podľa hodnotenia.
- Vyhľadávanie podľa surovín
- Stránkovanie zoznamu receptov cez AJAX.
- Prepočet množstva surovín podľa zvoleného počtu porcií.
- Blokovanie používateľov administrátorom.
- Nahrávanie obrázka cez drag & drop s náhľadom pred odoslaním.
- Vlastné CSS s pokročilými vlastnosťami (premenné, nesting, grid, media queries) a vlastné riešenie responzivity bez frameworku
- Externé API - napr. načítanie nutričných hodnôt surovín alebo „recept dňa“ z TheMealDB.
- Pokročilá kontrola formulárov na strane klienta (živá validácia počas písania).
