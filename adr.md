# Felhőnatív, domain alapú mikroszolgáltatás architektúra alkalmazása

## Kontextus és problémafelvetés

A GreenRide egy városi mikromobilitási platform, amelyben a felhasználói működés, a járművek kezelése, az utazások indítása és lezárása, a fizetés, a flottamenedzsment és az ügyféltámogatás egyszerre vannak jelen. A rendszer több külső szolgáltatással is együttműködik, például térképes, fizetési, azonosítási és értesítési megoldásokkal, valamint közvetlen kapcsolatban áll a járművek IoT eszközeivel is.

A platformnak magas rendelkezésre állást kell biztosítania, mert a szolgáltatás közvetlenül a felhasználók mindennapi közlekedését támogatja. Emellett a rendszernek hosszabb távon jelentős növekedést is kezelnie kell, ezért fontos a jó skálázhatóság. Különösen érzékeny pont a járműkeresés és a jármű feloldása, mert ezek közvetlenül hatnak a felhasználói élményre. A döntési kérdés az volt, hogy milyen architektúra támogatja ezt a legjobban hosszú távon.

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
* Felhőnatív, domain alapú mikroszolgáltatás architektúra

## Döntés eredménye

Választott opció: "Felhőnatív, domain alapú mikroszolgáltatás architektúra", mert ez támogatja legjobban a magas rendelkezésre állást, a fokozatos skálázást, valamint a kritikus üzleti folyamatok külön optimalizálását.

### Következmények

* Jó, mert a fő üzleti területek külön szolgáltatásokként jelenhetnek meg, ezért a felhasználókezelés, a járműkezelés, az utazáskezelés, a fizetés és a flottamenedzsment egymástól elkülönülten fejleszthető.
* Jó, mert az egyes szolgáltatások külön skálázhatók a saját terhelésük szerint, így a járműkeresés és az utazáskezelés nem ugyanúgy terheli a rendszert.
* Jó, mert a kritikus folyamatok, például a járműkeresés és a jármű feloldása külön optimalizálhatók.
* Jó, mert a külső integrációk jobban szétválaszthatók a belső üzleti logikától, így például a fizetés, az értesítések és az IoT kapcsolatok tisztábban kezelhetők.
* Jó, mert a rendszer későbbi bővítése egyszerűbb, ha új üzleti funkció vagy új integráció jelenik meg.
* Rossz, mert az architektúra üzemeltetése és felügyelete összetettebb, mint egy monolit rendszer esetén.
* Rossz, mert több szolgáltatás között nehezebb az adatkonzisztencia kezelése.
* Rossz, mert a hibakeresés és a szolgáltatások közötti kommunikáció követése bonyolultabb.
* Rossz, mert a megoldás nagyobb tervezési fegyelmet igényel, főleg az interfészek és a szolgáltatáshatárok meghúzásánál.

### Megerősítés

A döntés megfelelősége a C4 modellben ellenőrizhető azzal, hogy a rendszer külön konténerekre és üzleti területekre bontva jelenik meg. Az ADR teljesülését az mutatja, ha a fő területek, például a felhasználókezelés, a járműkezelés, az utazáskezelés, a fizetés, az értesítések és a flottamenedzsment önálló szolgáltatásként szerepelnek. Ezt az is megerősíti, ha a kritikus folyamatok külön optimalizálhatók, például a gyors járműkeresés cache segítségével, vagy az események aszinkron kezelése üzenetkezelőn keresztül.

### Kapcsolódás a szakirodalomhoz
A választott megoldás Ian Sommerville Software Engineering című könyvében bemutatott szempontokkal is összhangban van. A Chapter 6 – Architectural design szerint az architektúrát a fő szerkezeti döntések és a nem funkcionális követelmények alapján kell kialakítani. A Chapter 17 – Distributed software engineering az elosztott rendszerek skálázhatóságát és összetettségét emeli ki, míg a Chapter 18 – Service oriented software engineering a szolgáltatásokra bontott felépítést támogatja. A Chapter 13 – Security engineering és a Chapter 14 – Resilience engineering pedig a biztonság és a folyamatos működés fontosságát erősíti meg.

## A vizsgált lehetőségek előnyei és hátrányai

### Monolitikus architektúra

A teljes rendszer egyetlen alkalmazásként valósul meg, közös üzleti logikával és tipikusan közös adatbázissal.

* Jó, mert egyszerűbb megvalósítani kisebb rendszerek esetén.
* Jó, mert kezdetben kisebb az üzemeltetési bonyolultság.
* Jó, mert rövid távon gyors fejlesztést tehet lehetővé.
* Jó, mert egy beadandó szintjén könnyebben átlátható lehet a teljes működés.
* Rossz, mert nehéz külön skálázni a nagy terhelésű funkciókat.
* Rossz, mert egy hiba nagyobb eséllyel hat az egész rendszer működésére.
* Rossz, mert a külső integrációk és az IoT funkciók növelik a kapcsoltságot és a komplexitást.
* Rossz, mert a hosszabb távú bővítés során a különböző üzleti területek könnyen túl szorosan összekapcsolódnak.

### Moduláris monolit architektúra

A rendszer logikailag modulokra bontott, de fizikailag egyetlen alkalmazásként kerül telepítésre.

* Jó, mert jobban strukturálható, mint a tiszta monolit megoldás.
* Jó, mert egyszerűbb üzemeltetni, mint a mikroszolgáltatásokat.
* Jó, mert jó átmeneti megoldás lehet közepes összetettségű rendszerekhez.
* Jó, mert a domének szétválasztása már tervezési szinten megjelenhet.
* Semleges, mert bizonyos mértékig javítja a karbantarthatóságot.
* Rossz, mert a skálázás továbbra sem történik finoman, funkciónként elkülönítve.
* Rossz, mert a magas rendelkezésre állás és a hibák izolációja korlátozottabb.
* Rossz, mert hosszú távon kevésbé támogatja a gyorsan növekvő, több üzleti területre épülő platformot.
* Rossz, mert a valós idejű járműkezelés, a fizetés és az IoT integráció együtt már túl sok felelősséget tolhat egyetlen telepítési egységbe.

### Felhőnatív, domain alapú mikroszolgáltatás architektúra

A rendszer üzleti területek szerint elkülönített, önállóan fejleszthető és telepíthető szolgáltatásokból áll.

* Jó, mert jól illeszkedik a rendszer természetes üzleti területeihez.
* Jó, mert támogatja a magas rendelkezésre állást és a hibatűrést.
* Jó, mert az egyes szolgáltatások külön skálázhatók.
* Jó, mert a kritikus üzleti folyamatok külön optimalizálhatók.
* Jó, mert a külső szolgáltatókhoz kapcsolódó logika jobban elkülöníthető.
* Jó, mert jobban támogatja a későbbi bővítést és a fokozatos továbbfejlesztést.
* Rossz, mert nagyobb tervezési fegyelmet és világos interfészeket igényel.
* Rossz, mert összetettebb az üzemeltetés és a monitorozás.
* Rossz, mert az elosztott működés miatt bonyolultabb a kommunikáció és a konzisztencia kezelése.
