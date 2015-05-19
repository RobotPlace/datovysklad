# Introduction #

Add your content here.

Description how to stream data:

http://jahodova.homeip.net/id/system_phpCommunicationStreaming_switchOnOff/type:1/
- zavoláte tuto URL v prohlížeči a streaming se v pozadí zapne. Stránka se bude nekonečně dlouho načítat,takže po chvíli okno zavřete

http://jahodova.homeip.net/id/system_phpCommunicationStreaming_switchOnOff/type:0/
- pokud streaming chcete na pozadí ukončit, zavolejte tuto URL.

Změnou je, že věta nemá na začátku $, který to nechce zkrátka akceptovat. Vyzkoušejte si to zatím přes ten Hercules. Funguje třeba toto:

Řešení 1) (varianta je nefunkční, protože je odstraněna nutnost vyplňovat na začátku název tabulky)

zápis do jediné tabulky:
DATAD,james,1234,Tool\_COM5,tlak
100
...
23
exit

nebo

DATAS,james,1234,Tool\_COM5,tlak
100
...
23
exit

Řešení 2)
A a B jsou na serveru. Bere to data:

S,1,1,25**M,1,25,25,25,25,25,25**

Modes 25 a 26 vrací ID tabulek:
tlak;32
teploty;101

## Úvahy nad rozšířením ##

Zítra tři možné varianty A B C D (jen nějaké se zavedou):

Posílání dat do Java appletu:
- příkazy viz mode 20 až 23
- připojení na stream viz mode 1 a 2
- zjištění žádaných dat ve streamu:

**Způsoby získání seznamů, hodnot a způsoby samotného streamování**

Tyto způsoby jsou pouze pro TCP protokol. UDP protokol musí mít u streamovaných dat ID (nejlépe před kódem věty).

Např.:
> TCP: $DSS,1,1,25
> UDP: $987564,DSS,1,1,25

A) Pro tabulky o jednom sloupci: (řešeno v mode=29, 30)
  * $DSS,1,1,25
  * $DSS,1,2,35
  * $DSS,1,1,26
  * $DSS,1,2,30
  * $DSS,1,5,152
> ...
  * $DSS, odpovídá hlavičce příkazu DataStreamSingle,
  * první číslo vždy odpovídá číslu tabulky,
  * druhé je pořadí hodnoty v tabulce,
  * třetí je hodnota
  * "**" je zakončení příkazu**

B) Pro tabulky o více sloupcích: (řešeno v mode=29, 30)
  * $DSM,1,25,25,25,25,25,25
  * $DSM,2,25,25,25,25,25,25
  * $DSM,2,25,25,25,25,25,25
  * $DSM,4,25,25,25,25,25,25
  * $DSM,1,25,25,25,25,25,25
> ...
  * $DSM, odpovídá hlavičce příkazu DataStreamMulti,
  * první číslo vždy odpovídá číslu tabulky,
  * druhé a další je pořadí hodnot/sloupců v tabulce,
  * "**" je zakončení příkazu**

C) Alternativa k A) a B)
  * S,1,25*** S,4,35**
  * S,3,30*** S,5,152**
> > ...
> > S, odpovídá hlavičce příkazu Stream,
  * druhé je ID hodnoty nebo tabulky (ID pak musí být unikátní pro tabulku i sloupec hodnoty a nedají se zaměnit),
  * třetí je hodnota
  * "**" je zakončení příkazu**

D) Pro zápis do různých tabulek o více sloupcích:
  * S,1,2,25*** S,3,1,35**
  * S,1,2,26*** S,2,10,30**
  * S,5,4,152

B je přehlednější, ale C a D jsou kratší.

E) UDP varianta

> bude mít před větami pro TCP uvedeno následující:

> add A) @timestamp$DSS,1,1,25**> add B) @timestamp$DSM,1,25,25,25,25,25,25**
> add C) @timestamp$S,1,25**> add D) @timestamp$S,1,2,25**

> timestamp = 135856.725 (hhmmss.ms)

> Zařízení posílající data stream při UDP pošle každou větu 3x a zařízení přijímající si data pro konkrétní tabulku odfiltruje(pro číselné zobrazení)/setřídí(pro graf) podle timestamp. Nová příchozí data s timestamps již existujícími se zahodí.

Ke Streamu a Depositu mne napadá, že by stačilo při zápisu kontrolovat periodu ukládání u Tabulek určených pouze pro Deposit a nahradit dva příkazy ("DATAS", "DATAD") jedním "S" jako Stream.

Přidělení ID tabulkové hodnotě probíhá:

a) v Drone
Applet zašle dotaz na Drone na Seznam Tabulek a Hodnot
> _GetTab_
Drone zašle:
> _DroneTab1,NazevTab,NazevVal,NazevVal,NazevVal,NazevVal,NazevVal_
> _DroneTab2,NazevTab,NazevVal,NazevVal,NazevVal_
> _DroneTab3,NazevTab,NazevVal,NazevVal,NazevVal,NazevVal,NazevVal_
> _DroneTab4,NazevTab,NazevVal,NazevVal_
v Appletu se provede výběr NazevVal seskupených podle NazevTab a odešle se požadavek na Drone
> _GetVal,NazevVal_
Drone odpoví potvrzením a vygenerováným ID pro NazevVal
> _DroneVal,NazevVal,ID_

b) Serveru
Applet zašle dotaz na Server na Seznam Tabulek a Hodnot
> mode=
Server zašle seznam Tabulek
> NazevTab
> NazevTab
> NazevTab
Applet zašle dotaz na Server na Seznam hodnot vybrané tabulky
> mode=
Server zašle seznam Tabulek
> NazevVal
> NazevVal
> NazevVal
v Appletu se provede výběr NazevVal seskupených podle NazevTab a odešle se požadavek na Drone
> _GetVal,NazevVal_
Drone odpoví potvrzením a vygenerováným ID pro NazevVal
> _DroneVal,NazevVal,ID_


Parsování dat a určení zda se jedná o A), nebp B) se bude řešit na základě prvního kódu DSS, nebo DSM.