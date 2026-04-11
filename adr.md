
# Felhőnatív, domain-alapú mikroszolgáltatás-architektúra alkalmazása

## Kontextus és problémafelvetés

A GreenRide egy városi mikromobilitási platform, amely felhasználók, járművek, fizetési folyamatok, flottakezelés és külső szolgáltatások együttműködésére épül. A rendszernek magas rendelkezésre állást, nagyfokú skálázhatóságot és jó teljesítményt kell biztosítania a kritikus üzleti folyamatokban, különösen a járműkeresés és a jármű-feloldás során. A döntési kérdés az volt, hogy milyen architektúra támogatja ezt a legjobban hosszú távon.

## Döntési szempontok

* magas rendelkezésre állás
* horizontális skálázhatóság
* jó teljesítmény a kritikus üzleti folyamatokban
* külső rendszerek integrálhatósága
* karbantarthatóság és gyors változtathatóság
* üzleti domainek természetes elkülönülése

## Vizsgált lehetőségek

* Monolitikus architektúra
* Moduláris monolit architektúra
* Felhőnatív, domain-alapú mikroszolgáltatás-architektúra

## Döntés eredménye

Választott opció: "Felhőnatív, domain-alapú mikroszolgáltatás-architektúra", mert ez támogatja legjobban a magas rendelkezésre állást, a fokozatos skálázást, valamint a kritikus üzleti folyamatok külön optimalizálását.

### Következmények

* Jó, mert a különálló domainekhez tartozó funkciók egymástól függetlenül fejleszthetők és módosíthatók.
* Jó, mert az egyes szolgáltatások külön skálázhatók a terhelésüknek megfelelően.
* Jó, mert a kritikus folyamatok, például a járműkeresés és a jármű-feloldás célzottan optimalizálhatók.
* Jó, mert a külső integrációk jobban elszigetelhetők a belső üzleti logikától.
* Rossz, mert az architektúra üzemeltetése és felügyelete összetettebb, mint egy monolit rendszer esetén.
* Rossz, mert több szolgáltatás között nehezebb az adatkonzisztencia és a hibakeresés kezelése.

### Megerősítés

A döntés megfelelősége a C4 modellben ellenőrizhető azzal, hogy a rendszer külön konténerekre és domainekre bontva jelenik meg. Az ADR teljesülését igazolja, ha a fő üzleti területek — például felhasználókezelés, járműkezelés, utazáskezelés, fizetés és flottamenedzsment — önálló szolgáltatásként jelennek meg, és a kritikus folyamatok elkülönítetten optimalizálhatók.

## A vizsgált lehetőségek előnyei és hátrányai

### Monolitikus architektúra

A teljes rendszer egyetlen alkalmazásként valósul meg, közös üzleti logikával és tipikusan közös adatbázissal.

* Jó, mert egyszerűbb megvalósítani kisebb rendszerek esetén.
* Jó, mert kezdetben kisebb az üzemeltetési bonyolultság.
* Jó, mert rövid távon gyors fejlesztést tehet lehetővé.
* Rossz, mert nehéz külön skálázni a nagy terhelésű funkciókat.
* Rossz, mert egy hiba nagyobb eséllyel hat az egész rendszer működésére.
* Rossz, mert a külső integrációk és az IoT funkciók növelik a kapcsoltságot és a komplexitást.

### Moduláris monolit architektúra

A rendszer logikailag modulokra bontott, de fizikailag egyetlen alkalmazásként kerül telepítésre.

* Jó, mert jobban strukturálható, mint a tiszta monolit megoldás.
* Jó, mert egyszerűbb üzemeltetni, mint a mikroszolgáltatásokat.
* Jó, mert jó átmeneti megoldás lehet közepes összetettségű rendszerekhez.
* Semleges, mert bizonyos mértékig javítja a karbantarthatóságot.
* Rossz, mert a skálázás továbbra sem történik finoman, funkciónként elkülönítve.
* Rossz, mert a magas rendelkezésre állás és a hibák izolációja korlátozottabb.
* Rossz, mert hosszú távon kevésbé támogatja a gyorsan növekvő, több doménre épülő platformot.

### Felhőnatív, domain-alapú mikroszolgáltatás-architektúra

A rendszer üzleti domainek szerint elkülönített, önállóan fejleszthető és telepíthető szolgáltatásokból áll.

* Jó, mert jól illeszkedik a rendszer természetes domainjeihez.
* Jó, mert támogatja a magas rendelkezésre állást és a hibatűrést.
* Jó, mert az egyes szolgáltatások külön skálázhatók.
* Jó, mert a kritikus üzleti folyamatok külön optimalizálhatók.
* Rossz, mert nagyobb tervezési fegyelmet és világos interfészeket igényel.
* Rossz, mert összetettebb az üzemeltetés és a monitorozás.
* Rossz, mert az elosztott működés miatt bonyolultabb a kommunikáció és a konzisztencia kezelése.
