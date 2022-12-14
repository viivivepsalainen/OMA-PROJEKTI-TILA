# OMA-PROJEKTI-TILA

Moduuli/tila on tehty Tero Karvisen Palvelinten hallinta -kurssille syksyllä 2022. 

Käytössä Asus Zenbook Windows 11 käyttöjärjestelmällä, AMD Ryzen 7 prosessorilla ja 8Gt fyysistä muistia.

Käytin Oracle VM:n kautta Linuxin ubuntupalvelinta sekä Ubuntu desktoppia testatakseni, että homma toimii.

Tarkoitus asentaa vanhemman ihmisen arjen helpotusta varten hänelle tarpeellinen sovellus/nettisivu saltin avulla. Tässä tapauksessa vanhempi ihminen tahtoo katsella netflixiä, muttei osaa käyttää tietokonetta, joten luodaan komento, jolla tietokone lataa Firefoxin selaimen ja avaa tämän jälkeen Netflixin sivun.

Alunperin tarkoitus oli ladata hänelle myöskin Spotify sekä Netflixin itse sovellus, mutta niissä tulikin suurempia ongelmia vastaan, kun spotifyn kaikki gpg -avaimet mitä löysin netistä olivat vanhentuneet. Netflixin kohdalla taas selvisi, että sillä ei ole ollenkaan appia Linuxille, vaan Netflixiä täytyy katsoa verkkoselaimen kautta. **Loppujenlopuksi päädyin siis luomaan tilan, joka lataa firefoxin selaimen sekä konfiguroi siellä kotisivuksi netflixin.**

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

Skriptiä ajaessa kaikki muu toimi normaalisti (teksti tuli ja Netflixin sivu avautui), mutta Firefoxin kohdalla tuli paljon virheilmoituksia: "Failed to load canberra-gtk-module" ja "missing chrome or resource url". Nämä sainkin selvitettyä, että johtuivat siitä, että Firefoxissa on sisäänrakennettu päivitysohjelma. Virheilmoitus oli kuitenkin hyvälaatuinen eikä ongelma. (https://www.reddit.com/r/Ubuntu/comments/wsnou2/missing_chrome_or_resource_url/).

Kuitenkin halusin saada selville, onnistuuko firefoxin lataus varmasti, joten poistin sen desktopista komennolla:

```sudo snap remove firefox```

Tämän jälkeen skriptiä uudestaan kokeillessani, tuli ilmoitus että komento "script" tarvitsee firefoxin ladattuna valmiiksi, jotta komento voidaan ajaa, joten latasin firefoxin takaisin komennolla:

```sudo snap install firefox```

Tämän jälkeen saimme error: unable to contact snap store. Tämä vissiin johtui siitä, että snap store on alhaalla (https://status.snapcraft.io/).

![down](https://user-images.githubusercontent.com/118457367/207634449-a5c4efab-a2e5-479a-a211-fb7e5df06ce8.jpg)

Koska tuo snap-store oli alhaalla, piti firefox latailla takaisin muita teitä pitkin. Kokeilin ensin ladata mozillan omien sivujen kautta lisäämällä gpg -avaimen sekä kansion ubuntulleni, mutta kansiota lisätessä jotain meni pieleen (en tiedä johtuiko omasta hitaasta netistä), mutta kansion lisäys aikakatkaistiin automaattisesti. Kokeiltuani pari kertaa, päätin ladata firefoxin flatpakin avulla. 

Flatpak oli itselleni ainakin uusi tuttavuus, mutta se on tosiaan ohjelmien asentamiseen ja hallintaan suunniteltu työkaluohjelmisto. 

Ensin latasin ohjelmiston:

```sudo apt install flatpak```

jonka jälkeen latasin flatpakin laajennuksen, joka mahdollistaa ohjelmien lataamisen ilman komentoriviä:

```sudo apt install gnome-software-plugin-flatpak```

ja viimeseinä vielä lisäsin Flathub -kansion, josta ohjelmat voidaan ladata:

```flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo```

Sitten vain komennolla:

```flatpak install flathub org.mozilla.firefox```

latailin firefoxin, joka onnistui. (https://support.mozilla.org/en-US/kb/install-firefox-linux , https://flatpak.org/setup/Ubuntu) 

Ja tämä Firefoxihan asentui ja avautui normaalisti, mutta meidän skriptille se ei käynyt, vaan vaati edelleen firefoxin lataamista snap storen avulla. Kokeiltiin vielä komennolla 

```snap refresh```

josko auttaisi, tämän jälkeen ```snap install firefox```, ja sehän auttoi, eli äskeinen flatpakin kanssa säätäminen oli täysin turhaa (joten poistin flatpakin lataaman firefoxin.)

Tämän jälkeen päätin, että firefoxin lataaminen ja netflixin sivun avaaminen on vähän liian helppo homma, joten päätin konffata firefoxin asetuksia niin, että firefoxin kotisivu onkin netflixin sivu).

Muokkasin ensimmäisenä firefoxiin kotisivuksi tuon netflixin sivun, jonka ajattelin auttavan asiaa. 

Tämän jälkeen etsin ikuisuuden oikeaa tiedostoa, jonne muokata kotisivun tiedot (kokeilin esim. apturl.js tiedoston muokkausta), ja muokkailin ties mitä minne, kunnes vihdoin ja viimein tajusin etsiä tuolla ```find -printf "%T+ %p\n"|sort``` komennolla, josko löytäisin oikean tiedoston, jota minun pitää muokata. 

Oikea tiedosto löytyi (toivottavasti) ja avautui, ja nyt lähden muokkailemaan sinne netflixin sivun tietoja. Huomasin, että tieto netflixin sivusta oli tietenkin päivittynyt sinne automaattisesti:

![homepage](https://user-images.githubusercontent.com/118457367/207673410-2473f472-3b14-4306-9072-10a557608310.jpg)

Sitten alkoi pohdinta, miten saan tämän kaiken skriptiin.

Ensi töikseni menin muokkailemaan skriptiä, että nyt sivu ei avaudukaan uudella komennolla, vaan että asetukset on jo valmiiksi ladatussa selaimessa.

Fiksuna tyttönä tajusin kopioida konfigurointitiedoston samaan paikkaan (/usr/local/bin), jossa skripti myöskin on. Nyt luodaan vielä init.sls tiedosto. 

Loin tosiaan tuon init.sls tiedoston:

![init sls](https://user-images.githubusercontent.com/118457367/207692683-9b71760c-8c70-4193-a8c9-7a1b8bd89564.jpg)

Testailin että minion hereillä, ekan state.applyn tulos failed:

![failed](https://user-images.githubusercontent.com/118457367/207692794-8d00ba10-395b-4048-8bbf-8cedb8760a1c.jpg)

Eli jos ymmärsin oikein, virheilmoituksen mukaan nuo tiedostojen sijainnit on vielä vähän hukassa, let's try again. 

Sain ensimmäisen virheen eli itse skriptitiedoston siirtymään minionille, mutta tuo firefoxin konffaustiedosto jäi vielä punaiselle, virheenä tuli "parent directory not present", lets see. 

Muuttelin hieman polkuja tiedostoihin ja kokeilen uudelleen, lopputuloksena toimii:

![toimii21](https://user-images.githubusercontent.com/118457367/207697087-f7820862-59ea-4c45-9a1a-be2aeeebba1f.jpg)

