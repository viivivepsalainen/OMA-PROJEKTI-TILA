# OMA-PROJEKTI-TILA

Aloitin tosiaan aluksi Firefoxin parissa. 

Ensin latasin itselleni kokonaan uuden Ubuntu -palvelimen, jotta saan aloitettua puhtaalla pöydällä. Latasin myöskin palvelimelle Saltstackin, jotta moduulin teko onnistuu. Tarkastin vielä, että minion oli hereillä ja toimii.

<img width="256" alt="image" src="https://user-images.githubusercontent.com/118457367/206497242-609821e4-4c47-4f44-86d5-054e049445a8.png">

Ensimmäisenä latailin tuon Firefoxin masterille, josta tarkoitus lähteä niitä asentelemaan minionille. 

Ensimmäisenä Firefoxin lataus itselleni. ELi asensin sitä itselleni tuolla:

```sudo apt install firefox```

Loin aluksi skriptin (joka kertoi että olet lataamassa Firefoxia ja lataaa sen), jonka testasin että toimii ja lisäsin minionille (state.apply). Sitten heräsin siihen, etten saa ubtuntu serverillä auki sitä nettisivua, joten päätin ladata ubuntu desktopin asioiden helpottamiseksi. Jatkuu huomenna 8.12.
os
Homma tosiaan jatkui vasta 14.12, joten nyt yritetään uudelleen. Ensin latailin sen Ubuntu desktopin (https://ubuntu.com/download/desktop). 

Latailin tosiaan tuota salt-minionia ja -masteria tuonne desktopille, jotta voin kokeilla toimiiko.

```sudo apt-get install salt-minion```

Muokkasin /etc/salt/minion nano -tiedostoon masterin tiedot sekä laitoin id minion1 ja käynnistelin minionia uudelleen, jonka jälkeen vielä hyväksyin minion1 avaimen masterille. 

Tämän jälkeen alkoi skriptin luominen ensin itselleni, jotta pääsen testaamaan toimiiko se. Skripti näyttikin siis tältä:

![moduuliscript](https://user-images.githubusercontent.com/118457367/207630810-9861abb7-63c3-4ac4-aee2-ce5925dd3439.jpg)

Skriptiä ajaessa kaikki muu toimi normaalisti (teksti tuli ja Netflixin sivu avautui), mutta Firefoxin kohdalla tuli paljon virheilmoituksia: "Failed to load canberra-gtk-module" ja "missing chrome or resource url". Nämä sainkin selvitettyä, että johtuivat siitä, kun Firefoxissa on ns. built-in päivittäjä, joten sitä ei erikseen pysty päivitellä terminaalissa (https://www.reddit.com/r/Ubuntu/comments/wsnou2/missing_chrome_or_resource_url/ lähteenä tiedolle reddit, joka hieman kyseenalainen).




