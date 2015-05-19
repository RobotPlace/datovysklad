# Principles #

This site propose you a posibility to integrate its properties into your application.

Summary:
| **Basic info** | **Description** |
|:---------------|:----------------|
| mode=1         | čtení položek TOOL (IP adresa)|
| mode=2         | čtení položek TOOL (IP port) |
| mode=3         | čtení položek TOOL (detaily) |
| mode=4         | úprava status action TOOL |
| mode=5         | ověření přihlašovacích údajů |
| mode=6         | výpis povolených TOOL: user je (vlastník, administrátor) |
| mode=7         | výpis povolených TOOL user je (ve skupině oprávněných)   |
| mode=8         | výpis zvolené trasy WPSET TOOL |
| mode=9         | výpis souhrnných informací TOOL |
| mode=10        | výpis textu Popisu 1 a Popis 2 TOOL |
| mode=11        | seznam rezervovaných tools |

**Oblasti a trasy**
| **Stažení** | **Description** |
|:--------------|:----------------|
| mode=14       | stažení bodů hranice oblasti skladu (Decimal Degrees) |
| mode=15       | stažení bodů hranice oblasti skladu (Degrees) |
| mode=16       | stažení bodů hranice oblasti skladu (GPS Coordinate) |
| mode=17       | stažení bodů route WPSET (Decimal Degrees) |
| mode=18       | stažení bodů route WPSET (Degrees) |
| mode=19       | stažení bodů route WPSET (GPS Coordinate) |

**Datové tabulky**
| **Založení**| **Description** |
|:--------------|:----------------|
| mode=12       | založení tabulek (data stream) |
| mode=13       | založení tabulek (data deposit) |
| mode=24       | založení tabulek GPS\_tracking |
| **Výpis**    | **Description** |
| mode=20       | výpis názvů tabulek TOOL uživatele |
| mode=21       | výpis ID limitů tabulek TOOL uživatele |
| mode=22       | výpis hodnot limitů tabulek TOOL uživatele |
| mode=23       | výpis seznamu sloupců pro danou tabulku |
| mode=25       | výpis všech datových tabulek (Data Deposit) |
| mode=26       | výpis všech datových tabulek pro (Data Stream) |
| **Zápis**    | **Description** |
| mode=29       | zápis dat do tabulek (styl "vše") |
| mode=30       | zápis dat do tabulek (styl "výběr") |
| **Stažení** | **Description** |
| mode=27       | stažení dat tabulky jako soubor TXT |
| mode=28       | stažení dat tabulky jako soubor CSV |
| mode=29       | zápis dat do tabulek (styl "vše")  |
| mode=30       | zápis dat do tabulek (styl "výběr") |
| **Autorizace**| **Description** |
| mode=31       | získání token k zařízení a tabulkám |
| mode=32       | ověření token k zařízení a tabulkám |

Exemple of VB.NET code:
```
Char result =  http://jahodova.homeip.net/id/system_phpCommunication/?mode=1&user=freetool&pass=freetool&tool=Tool_COM5 
```

# PHP modes detail descriptions #

## mode=1 ##
čtení položek TOOL (IP adresa):

Try this exemple of a link:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=1&user=freetool&pass=freetool&tool=Tool_COM5

Exemple of output ERRORS:
```
 ERROR:1000 - špatné přihlašovací údaje
 ERROR:1001 - nic nenalezeno (nebo nedostatečné oprávnění)
 ERROR:1002 - nalezeno vice polozek nez 1
```

## mode=2 ##
čtení položek TOOL (IP port):

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=2&user=UZIVATEL&pass=HESLO&tool=XYZ

VÝSTUP: IP port

  * ERRORS:
  * ERROR:1000 - špatné přihlašovací údaje
  * ERROR:1001 - nic nenalezeno (nebo nedostatečné oprávnění)
  * ERROR:1002 - nalezeno vice polozek nez 1

## mode=3 ##
čtení položek TOOL (detaily):

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=3&user=UZIVATEL&pass=HESLO&tool=XYZ

Výčet detailů daného tool. Na každém řádku 1 atribut

  * ERRORY:
  * ERROR:1000 - špatné přihlašovací údaje
  * ERROR:1001 - nic nenalezeno (nebo nedostatečné oprávnění)
  * ERROR:1002 - nalezeno vice polozek nez 1

## mode=4 ##
Úprava status action:

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=4&user=UZIVATEL&pass=HESLO&tool=XYZ&status_action=0

VÝSTUPY: 1

  * 1 - provedeno
  * ERROR:1000 - špatné přihlašovací údaje
  * ERROR:1001 - nic nenalezeno
  * ERROR:1002 - nalezeno více položek než 1
  * ERROR:1003 - chyba při úpravě
  * ERROR:1004 - není právo upravovat

příklad status\_action
0 offline
1 online without reservation
2 online and reservation
3 operating
4 operating finished

## mode=5 ##
Ověření přihlašovacích údajů:

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=5&user=UZIVATEL&pass=HESLO

VÝSTUP:  0/1


## mode=6 ##
Výpis tools, kde jsem vlastník nebo administrátor:

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=6&user=UZIVATEL&pass=HESLO

VÝSTUP: Názvy tools. Na každém řádku 1.

  * ERRORY:
  * ERROR:1000 - špatné přihlašovací údaje

## mode=7 ##
Získání tools, kde jsem ve skupině oprávněných:

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=7&user=UZIVATEL&pass=HESLO

VÝSTUP: Názvy tools. Na každém řádku 1.

  * ERRORY:
  * ERROR:1000 - špatné přihlašovací údaje

## mode=8 ##
WPSET výpis zvolené trasy

Zde se souřadnicemi v systému souřadnic zvolených v detailech:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=8&user=hubacek&pass=A79Ch&tool=Tool_11_COM8

Příklad:

  * $WPSET,1,4959.4397,1444.4734,432,120,1,0,0\*checksum
  * $WPSET,2,4959.4397,1444.4608,432,0,1,0,0\*checksum

Zde kažný mode je pro jiný formát souřadnic:

1) Decimal Degrees:  mode=17
2) Degrees:          mode=18
3) GPS Coordinate:   mode=19

## mode=9 ##
Výpis souhrnných informací

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=9&user=hubacek&pass=A79Ch&tool=Tool_11_COM8

  * Tool name
  * Mezisklad name
  * Sklad name
  * IP adresa skladu
  * IP port meziskladu


Příklad:

  * Tool\_11\_COM8
  * ms\_2
  * s\_Mukarov\_hriste
  * 78.24.8.42
  * 0

## mode=10 ##
Výpis textu Popisu 1 a Popis 2

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?user=test&pass=test&mode=10&tool=sdvsdvsd2

Příklad:
TextPopisu189.176.83.50
TextPopisu2


## mode=11 ##
Seznam rezervovaných tools

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?mode=11&user=test&pass=test

## mode=12 + 13 ##
Založení tabulek:

**mode=12: data stream**
A possibility to stream any data to the server and store it with a no limit frequency rate (only the internet latency count and usualy varies between 7 and 200ms).

**mode=13: data deposit**
A possibility to "stream" any data to the server and store it with a limit frequency rate set to 10 seconds.

Modes 12,13 stejně jako 24 akceptují parametr „cols“ pro tvorbu tabulek o více sloupcích.

Try this:
http://jahodova.homeip.net/id/system_phpCommunication/?user=USER&pass=PASS&mode=12&tool=TOOL&table=NAZEV_TABULKY

http://jahodova.homeip.net/id/system_phpCommunication/?user=USER&pass=PASS&mode=13&tool=TOOL&table=NAZEV_TABULKY

NAZEV\_TABULKY: možno libovolné alfanumericke znaky bez diakritiky + podtržítko

  * 1 - založeno
  * ERROR:1003 - spatny nazev tabulky
  * ERROR:1004 - tabulka s nazvem pro uzivatele a tool jiz existuje
  * ERROR:1005 - prilis dlouhy nazev tabulky (cca max 40 znaku)
  * ERROR:1006 - limit 10 tabulek na uživatele
  * ERROR:1007 - chyba při vytváření

## mode=14 + 15 + 16 ##
Stažení bodů hranice oblasti skladu:

Obdobně jako je definována věta WPSET, kterou jsou zaslány souřadnice,
jsou vytvořeny 3 nové mody pro zaslání vět BDSET (boundery set) v následující
konfiguraci. Kažný mode je pro jiný formát souřadnic:

1) Decimal Degrees:
system\_phpCommunication/?mode=14&user=test&pass=test&tool=sdvsdvsd2

2) Degrees:
system\_phpCommunication/?mode=15&user=test&pass=test&tool=sdvsdvsd2

3) GPS Coordinate:
system\_phpCommunication/?mode=16&user=test&pass=test&tool=sdvsdvsd2

výsledkem je výčet vět pro každý bod:
$BDSET,cislo\_bodu,Lat,Lon,Ground\_Alt,Difference\_Alt1A

např:
  * $BDSET,1,5204.2754,413.3046,0,0,1A
  * $BDSET,2,5204.2904,413.3062,0,0,1A
  * $BDSET,3,5204.2962,413.3349,0,0,1A
  * $BDSET,4,5204.3124,413.3326,0,0,1A
  * $BDSET,5,5204.3175,413.3577,4,0,1A


## mode=17 + 18 + 19 ##
Stažení bodů route WPSET v různých souřadnicích:

1) Decimal Degrees:
system\_phpCommunication/?mode=17&user=test&pass=test&tool=sdvsdvsd2

2) Degrees:
system\_phpCommunication/?mode=18&user=test&pass=test&tool=sdvsdvsd2

3) GPS Coordinate:
system\_phpCommunication/?mode=19&user=test&pass=test&tool=sdvsdvsd2

## mode=20 + 21 + 21 + 22 + 23 ##
Stažení seznamů pro stažení dat

mode=20
Vypíše názvy tabulek pro daný tool a daného uživatele. Uživatel musí mít k tool práva.
system\_phpCommunication/?user=test&pass=test&mode=20&tool=sdvsdvsd2

mode=21:
Vypíše ID limitů pro danou tabulku daného tool. Uživatel musí mít k danému tool a tabulce práva.
system\_phpCommunication/?user=test&pass=test&mode=20&tool=sdvsdvsd2&table=tlak

mode=22:
Vypíše 5 hodnot pro daný limit na základě jeho ID. Uživatel musí mít práva k tool, ke kterému se váže tabulka a také práva k dané tabulce.
system\_phpCommunication/?user=test&pass=test&mode=20&tool=sdvsdvsd2&limit=1

mode=23:
Vypíše sloupce pro danou tabulku. Nyní konstantně 1
system\_phpCommunication/?user=test&pass=test&mode=20&tool=sdvsdvsd2&table=tlak

Try this:
http://gpsserver.sweb.cz/id/?mode=20&user=james&pass=1234&tool=Tool_COM5

## mode=24 ##
zakládá třetí typ tabulek gps\_tracking přiřazené i nepřiřazené Tool:

- V obou následujících případech jsou založny sloupce tlak a vyska.

1) Založí tabulku, která nebude připnutá k žádnému tool.
http://gpsserver.sweb.cz/id/?user=test&pass=test&mode=24&table=test&cols=tlak,vyska

2) Založí tabulku, která je připnutá k tool nazevTool.
http://gpsserver.sweb.cz/id/?user=test&pass=test&mode=24&table=test&cols=tlak,vyska&tool=nazevTool

ZDE:
http://hubacekp.dyndns.org/phpMyAdmin/ po přihlášení lze sledovat databázi
"phtools" (selekce vlevo) vidět vytvořené tabulky. Všechny které
začínají "xxx_" jsou právě tyto tabulky, které se vytváří přes MODEs.
Můžete si prohlížet jejich strukturu a případně data. Silné dporučení nic
nemazat, aby se neztratila konzistence dat._

## mode=25 + 26 ##
výpis všech datových tabulek k danému tool (k němuž mám oprávnění)
mode pro Data Deposit:
system\_phpCommunication/?user=test&pass=test&mode=25&tool=sdvsdvsd2

mode pro Data Stream:
system\_phpCommunication/?user=test&pass=test&mode=26&tool=sdvsdvsd2

## mode=27 + 28 ##
stažení dat tabulky jako soubor (již to fungue klikem na stránce)

mode pro TXT:
system\_phpCommunication/?user=test&pass=test&mode=27&tool=sdvsdvsd2&table=tlak

mode pro CSV:
system\_phpCommunication/?user=test&pass=test&mode=28&tool=sdvsdvsd2&table=tlak

## mode=29 + 30 ##
zadání v Mantis/[Issue 0000040](https://code.google.com/p/datovysklad/issues/detail?id=0000040)

zápis dat do tabulek A:

system\_phpCommunication/?user=test&pass=test&mode=29&tool=sdvsdvsd2&table=tlak&val=val1,val2
  * bude to platné jak pro tabulky s jedním, tak několika sloupci
  * pokud bude zapisováno více/méně dat než je sloupců, bude to chyba
  * pořadí hodnot bude vzestupně podle id sloupce hodnot v tabulce

zápis dat do tabulek B:

system\_phpCommunication/?user=test&pass=test&mode=30&tool=sdvsdvsd2&table=tlak&col=2,1,3&val=hodnota2,hodnota1,hodnota3
  * bude to platné jak pro tabulky s jedním (col=1), tak několika sloupci
  * odpovídající hodnota bude zapsána podle id sloupce hodnot v tabulce

id sloupce pro uživatelský zápis dat se určí podle pořadí výpisu sloupsů hodnot z mode=23 v tomto formátu:
```
tlak;1
teplota;2
```

Chybová hlášení:
```
ERROR:1003 – nenalezena tabulka 
ERROR:1004 – neznámý sloupec 
ERROR:1005 – málo sloupců k zápisu
```

## mode=31 ##
získání token k zařízení a tabulkám

MODE 31: akceptuje user,pass,tool:

GETrequest command:
> http://hobbydrone.com/system_phpCommunication/?mode=31&user=james&pass=1234&tool=DemoDevice

Exemple of output:
> 0
> token

## 32) mode=32 ##
ověření token k zařízení a tabulkám

MODE 32: akceptuje user,token,tool: vrací 0/1 (ověření správnosti tokenu)

GETrequest command:
> http://hobbydrone.com/system_phpCommunication/?mode=32&user=james&token=2PC9vrIjf73xOKGhd51QMokf7OpG&tool=DemoDevice

Exemple of output:
> 0 approved
  1. not approved