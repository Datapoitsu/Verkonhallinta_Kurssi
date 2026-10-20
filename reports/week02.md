# 1. Johdanto
Mikä on SNMP

    Simple network management protocll on nykyaikainen ohjelmisto, jonka aikana kertätään jatkuvasti tiettoa verkkolaitteista, palvelimista ja palveluista.


# 2. Asennus
Miten SNMP-agentti asennettiin?

    Palvelimesta käsin komennolla apt install snmp snmpd -y.

Mitä konfiguraatiomuutoksia tehtiin? 

    Muutettiin rocommunity (read-only-community) nimeksi public.

# 3. Kerätyt tiedot


Suoritetut SNMP-kyselyt 

    snmpwalk -v2c -c public web1 system


| Laite | Nimi | Käyttöjärjestelmä | Uptime |
|---------|---------|---------|---------|
| web1 | web1 | linux-ubuntu 24.04 | 0:14:48:27 |
| db1 | db1 | Linux Ubuntu 24.04.4 | 0:04:37.64 |
| branch-client | branch-client | Linux Ubuntu 24.04.4 | 0:01:18.75 |


# 4. Verkkorajapinnat

SNMP:n avulla kerätyt verkkorajapintatiedot 
    
    IF-MIB::ifDescr.1 = STRING: lo
    IF-MIB::ifDescr.139 = STRING: eth0
    IF-MIB::ifDescr.142 = STRING: eth1

    Kolme rajapintaa

Mikä rajapinta yhdistää laitteen verkkoon?

    Rajapinta nro 1. täytyy olla paikallinen rajapinta. Rajapinnat 139 ja 142 ovat ethernet yhteyksien kautta saapuvia. Myönnettävästi tietotaitoni ei riitä (en jaksa) tutkimaan, että kumpi oikeasti yhdistää laitteen verkkoon.


# 5. OID-analyysi.

| OID | Tarkoitus |
| --- | --- |
| `sysName.0` | Laitteen nimi. |
| `sysDescr.0` | Laitteen kuvaus |
| `sysUpTime.0` | Käynnissäoloaika |
| `ifDescr` | Rajapinnan nimi |
| `ifOperStatus` | Rajapinnan toimintatila |



# 6. Pohdinta.
Mitä opit tehtävän aikana?

    Verkkolaite asiat eivät ole oma vahvuuteni.


Mitä hyötyä SNMP:stä on verkonhallinnassa?

    SNMP mahdollistaa tarpeellisen tiedon keräämisen verkonhallinnassa. 

Mitä tietoa SNMP:n avulla voidaan kerätä?

    SNMP:n avulla kerätään tietoa verkkolaitteista, palvelimista ja palveluista. 


Mitä ongelmia yhteisöpohjaisessa SNMPv2:ssa on?

    Ei ole salattu. 

Missä tilanteissa käyttäisit mieluummin SNMPv3:a?

    Salattu, turvallisin. Sisältää käyttäjätunnistuksen ja viestien eheyden tarkistuksen. Aina.


# 7. Tekoälyn kätttö

Ihan törkeän paljon, taas ja vaihteeksi. En sanoisi, että mikään vastauksistani olisi tekoälyn kirjoittama, mutta saadakseni kaiken toimimaan pyysin siltä paljon apuja. Yksi mikä tuli vastaan oli se, että kontti ei salli yhteyttä ulos, joten vaihdon dns-palvelimen. Todennäköisesti dns-palvelimen vaihto on väärä tapa, mutta en jaksa ja haluan nukkumaan. Lopulta minulle aukesi, että yritin db1:een ja branch-clienttiin asentaa tarkkailuohjelmaa, kun pelkkä agentti olisi riittänyt. Koen oppineeni hieman paremmin SNMP:n toimintaa, vaikka parantamiseen olisi varaa huomattavasti.