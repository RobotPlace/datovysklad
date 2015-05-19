## Introduction ##




## Easy steps to start ##

Easy steps to Track any device

  1. Create one tracking table and name it
    1. založí tabulku, která nebude připnutá k žádnému Device
      * http://gpsserver.sweb.cz/id/system_phpCommunication/?user=test&pass=test&mode=24&table=test&cols=tlak,vyska
    1. založí tabulku, která je připnutá k device nazevDevice
      * http://gpsserver.sweb.cz/id/system_phpCommunication/?user=test&pass=test&mode=24&table=test&cols=tlak,vyska&tool=nazevDevice
  1. Send data to the table (NMEA-GPRMC, GPGGA or kml format) using Data deposit (GETrequest - mode=24)
    1. zápis dat do tabulek A:
      * http://gpsserver.sweb.cz/id/system_phpCommunication/?user=test&pass=test&mode=29&tool=sdvsdvsd2&table=tlak&val=val1,val2
      * bude to platné jak pro tabulky s jedním, tak několika sloupci
      * pokud bude zapisováno více/méně dat než je sloupců, bude to chyba
      * pořadí hodnot bude vzestupně podle id sloupce hodnot v tabulce
    1. zápis dat do tabulek B
      * http://gpsserver.sweb.cz/id/system_phpCommunication/?user=test&pass=test&mode=30&tool=sdvsdvsd2&table=tlak&col=2,1,3&val=hodnota2,hodnota1,hodnota3
      * bude to platné jak pro tabulky s jedním (col=1), tak několika sloupci
      * odpovídající hodnota bude zapsána podle id sloupce hodnot v tabulce
  1. Look on the map to see the tracking