# Rehvivahetuse broneerimissüsteemi testiplaan

Autor: Ken Elken  
Rakendus: Rehvivahetuse broneerimissüsteem  
Testitav keskkond: veebimajutus  

Avalik broneerimisleht: https://rehvivahetusebronn.gt.tc/index.php 
Administraatori sisselogimisleht: https://rehvivahetusebronn.gt.tc/login.php

Testimiseks on loodud eraldi administraatori kasutaja `testadmin`, parooliks `RehvTest2026!`

---

## 1. Rakenduse kirjeldus

**rehvivahetuse broneerimissüsteem**.

Rakendus on mõeldud selleks, et klient saaks veebilehel valida endale sobiva rehvivahetuse aja.
Teine, ilmselt põhiline miks seda rakendust vaja läheb, et admini õigusega kasutajatel oleks selge pilt ees kuna, kes ja mis tööd soovib.
Administraator saab süsteemis lisada avatud tööpäevi ja kellaaegu, ning muuta broneeringute staatust.

Rakenduse olulisemad funktsioonid:

1. klient saab valida sobiva kuupäeva ja kellaaja;
2. klient saab sisestada kontaktandmed ja auto info;
3. süsteem salvestab broneeringu andmebaasi;
4. administraator saab broneeringuid vaadata;
5. administraator saab lisada vabu päevi ja kellaaegu;
6. administraator saab muuta broneeringu staatust;
7. süsteem peaks saatma broneeringu kohta kinnituskirja.

---

## 2. Testimise eesmärk

Testimise eesmärk on kontrollida, kas rehvivahetuse broneerimissüsteemi põhifunktsioonid töötavad õigesti.

Testimisega kontrollitakse, kas klient saab broneeringu teha, kas süsteem kuvab ainult vabu aegu, kas broneering salvestub andmebaasi ning kas administraator saab broneeringuid hallata.

Samuti kontrollitakse, kas süsteem käitub õigesti veaolukordades, näiteks kui kasutaja jätab kohustusliku välja täitmata või proovib adminivaatesse siseneda valede andmetega.

Neid funktsioone on vaja testida, sest broneerimissüsteemi puhul on oluline, et klient ei saaks valida valet või juba hõivatud aega ning administraatoril oleks süsteemis õige ülevaade tehtud broneeringutest.

---

## 3. Testkeskkond ja testandmed

Testimine toimub veebibrauseris Google Chrome.

Testitav rakendus asub veebimajutuses.

| Leht | Aadress |
|---|---|
| Avalik broneerimisleht | https://rehvivahetusebronn.gt.tc/index.php |
| Administraatori sisselogimisleht | https://rehvivahetusebronn.gt.tc/login.php |

Testimiseks kasutatakse eraldi administraatori testkasutajat.

| Väli | Väärtus |
|---|---|
| Kasutajanimi | testadmin |
| Parool | RehvTest2026! |

Testimiseks kasutatakse järgmisi näidisandmeid:

| Väli | Väärtus |
|---|---|
| Nimi | Test Klient |
| Telefon | 55555555 |
| E-post | test@test.ee |
| Auto | BMW E46 |
| Registreerimisnumber | 123ABC |
| Rehvimõõt | 205/55R16 |
| Teenus | Täisvahetus |
| Lisainfo | Testbroneering koolitöö jaoks |

---

## 4. Testjuhtumid

| Nr | Testi nimetus | Testimise sammud | Oodatav tulemus | Tegelik tulemus | Märkused |
|---|---|---|---|---|---|
| 1 | Administraatori sisselogimine õigete andmetega | 1. Ava administraatori sisselogimisleht. <br> 2. Sisesta kasutajanimi `testadmin`. <br> 3. Sisesta õpetajale eraldi antud parool. <br> 4. Vajuta nuppu `Logi sisse`. | Administraator suunatakse broneeringute vaatesse. Test õnnestub, kui broneeringute nimekiri avaneb. | Õnnestus | Adminivaade avaneb. |
| 2 | Administraatori sisselogimine vale parooliga | 1. Ava administraatori sisselogimisleht. <br> 2. Sisesta kasutajanimi `testadmin`. <br> 3. Sisesta parooliks `valeparool`. <br> 4. Vajuta nuppu `Logi sisse`. | Süsteem ei lase kasutajat sisse ja kuvab veateate. Test õnnestub, kui adminivaatesse ei pääse. |  | Veaolukorra test. |
| 3 | Avatud päeva ja kellaaja lisamine adminivaates | 1. Logi administraatorina sisse. <br> 2. Ava päevade või kellaaegade haldamise vaade. <br> 3. Lisa uus avatud päev. <br> 4. Määra algus- ja lõpukellaaeg. <br> 5. Salvesta muudatus. | Lisatud päev ja kellaaeg salvestuvad süsteemi. Test õnnestub, kui klient näeb seda aega broneerimisvormis. | Õnnestus | Vajalik enne kliendipoolse broneeringu tegemist. |
| 4 | Broneeringu tegemine korrektsete andmetega | 1. Ava avalik broneerimisleht. <br> 2. Vali admini poolt lisatud kuupäev. <br> 3. Vali vaba kellaaeg. <br> 4. Sisesta nimi `Test Klient`. <br> 5. Sisesta telefon `55555555`. <br> 6. Sisesta e-post `test@test.ee`. <br> 7. Sisesta auto `BMW E46`. <br> 8. Sisesta registreerimisnumber `123ABC`. <br> 9. Sisesta rehvimõõt `205/55R16`. <br> 10. Vali teenus `Täisvahetus`. <br> 11. Vajuta broneerimise nuppu. | Süsteem salvestab broneeringu ja kuvab kasutajale kinnitusteate. Test õnnestub, kui broneering on nähtav ka administraatori vaates. | Õnnestus | Tavakasutuse test. |
| 5 | Kohustusliku välja tühjaks jätmine | 1. Ava broneerimisleht. <br> 2. Vali kuupäev ja kellaaeg. <br> 3. Jäta näiteks nimi või telefon tühjaks. <br> 4. Täida ülejäänud väljad. <br> 5. Vajuta broneerimise nuppu. | Süsteem ei salvesta puudulike andmetega broneeringut ja kuvab veateate. Test õnnestub, kui adminivaates uut broneeringut ei teki. |  | Veaolukorra test. |
| 6 | Sama aja topeltbroneerimine | 1. Tee esimene broneering kindlale kuupäevale ja kellaajale. <br> 2. Ava broneerimisleht uuesti. <br> 3. Vali sama kuupäev. <br> 4. Kontrolli, kas sama kellaaeg on veel valitav. <br> 5. Kui aeg on valitav, proovi teha teine broneering samale ajale. | Süsteem ei luba sama aega kaks korda broneerida. Test õnnestub, kui teist broneeringut samale ajale ei teki. |  | Piiri- või erijuhtumi test. |
| 7 | Broneeringu kuvamine adminivaates | 1. Tee kliendina uus testbroneering. <br> 2. Logi administraatorina sisse. <br> 3. Ava broneeringute nimekiri. <br> 4. Otsi broneeringut nimega `Test Klient`. | Tehtud broneering on adminivaates nähtav koos sisestatud andmetega. Test õnnestub, kui kuvatakse nimi, kuupäev, kellaaeg, auto info ja teenus. | Õnnestus |  |
| 8 | Broneeringu staatuse muutmine | 1. Logi administraatorina sisse. <br> 2. Ava broneeringute nimekiri. <br> 3. Leia testbroneering. <br> 4. Muuda broneeringu staatus näiteks väärtuseks `Tühistatud`. <br> 5. Salvesta muudatus. <br> 6. Uuenda lehte. | Broneeringu uus staatus jääb alles ka pärast lehe uuendamist. Test õnnestub, kui muudatus salvestub andmebaasi. | Õnnestus |  |
| 9 | Adminivaatesse minek ilma sisselogimata | 1. Logi administraatorina välja. <br> 2. Ava brauseris otse adminivaate aadress. | Süsteem suunab kasutaja tagasi sisselogimislehele. Test õnnestub, kui broneeringuid ei kuvata enne sisselogimist. |  | Turvalisuse test. |
| 10 | Kinnituskirja saatmine pärast broneeringut | 1. Ava avalik broneerimisleht. <br> 2. Tee uus broneering ja sisesta e-posti aadress. <br> 3. Kinnita broneering. <br> 4. Kontrolli sisestatud e-posti postkasti ja rämpsposti kausta. | Süsteem saadab broneeringu kohta kinnituskirja. Test õnnestub, kui kiri jõuab kasutaja e-posti aadressile. | Ebaõnnestus | Broneering salvestub, kuid kinnituskiri ei jõua kohale. Viga vajab SMTP/PHPMailer seadistuse kontrollimist. |

---

## 5. Testitavad olukorrad

Testiplaanis on kaetud erinevad olukorrad.

### Tavalised kasutusolukorrad

- administraator logib süsteemi sisse;
- administraator lisab avatud päeva ja kellaaja;
- klient teeb broneeringu;
- administraator vaatab broneeringut;
- administraator muudab broneeringu staatust.

### Veaolukorrad

- kasutaja jätab kohustusliku välja tühjaks;
- administraator sisestab vale parooli;
- kinnituskiri ei jõua kohale.

### Piiri- või erijuhtum

- kasutaja proovib broneerida sama aega teist korda.

### Turvalisuse olukord

- kasutaja proovib minna adminivaatesse sisselogimata.

---

## 6. Tulemuste hindamine

Test loetakse õnnestunuks, kui tegelik tulemus vastab oodatavale tulemusele.

Kui tegelik tulemus ei vasta oodatavale tulemusele, loetakse test ebaõnnestunuks ja probleem kirjeldatakse märkuste veerus.

Näiteks kui klient teeb broneeringu ja see ilmub administraatori vaatesse, siis on broneeringu salvestamise test õnnestunud.

Kui kinnituskiri pärast broneeringut kohale ei jõua, siis on kinnituskirja saatmise test ebaõnnestunud, kuigi broneering ise võib olla korrektselt salvestatud.

---

## 7. Leitud viga ja parandamise plaan

Testimise käigus selgus, et broneeringu tegemine salvestub korrektselt andmebaasi ja on administraatori vaates nähtav, kuid kinnituskiri ei jõua kasutaja e-posti aadressile.

Probleem on tõenäoliselt seotud e-posti saatmise seadistusega, PHPMailer või SMTP ühenduse andmetega.

Kuna broneering ise salvestub õigesti, ei takista see süsteemi põhifunktsiooni kasutamist, kuid kasutajamugavuse mõttes tuleks kinnituskirja saatmine parandada.

Pärast parandamist tuleb sama test uuesti läbi teha.


---

## 8. Kokkuvõte

Testimise käigus kontrolliti rehvivahetuse broneerimissüsteemi olulisemaid funktsioone.

Põhifunktsioonid, nagu administraatori sisselogimine, avatud aegade lisamine, broneeringu tegemine, broneeringu kuvamine ja staatuse muutmine, töötavad.

Testimise käigus ilmnes probleem kinnituskirja saatmisega. Broneering salvestub süsteemi ja on administraatori vaates nähtav, kuid e-kiri ei jõua kasutajani.

See tähendab, et süsteemi põhifunktsioon töötab, kuid e-posti saatmise seadistus vajab parandamist.

Kinnituskirja saatmise funktsioon on testiplaanis märgitud ebaõnnestunud testina, sest broneering salvestub kuid e-kiri hetkel kohale ei jõua.