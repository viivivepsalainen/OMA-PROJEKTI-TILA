# OMA-PROJEKTI-TILA
palvelinten hallinta s22, oman tilan/moduulin teko 

Käytössä Asus Zenbook Windows 11 käyttöjärjestelmällä, AMD Ryzen 7 prosessorilla ja 8Gt fyysistä muistia. 

Käytin Oracle VM:n kautta Linuxin ubuntupalvelinta, jotta saan sinne luotua herran ja orjan ja testata onnistuuko. 

Tarkoitus asentaa vanhemman ihmisen arjen helpotusta varten hänelle tarpeellinen sovellus/nettisicu saltin avulla. Tässä tapauksessa vanhempi ihminen tahtoo katsella netflixiä, muttei osaa käyttää tietokonetta, joten luodaan komento, jolla tietokone lataa Firefoxin selaimen ja avaa tämän jälkeen Netflixin sivun. 

Alunperin tarkoitus oli ladata hänelle myöskin Spotify sekä Netflixin itse sovellus, mutta niissä tulikin suurempia ongelmia vastaan, kun spotifyn kaikki gpg -avaimet mitä löysin netistä olivat vanhentuneet. Netflixin kohdalla taas selvisi, että sillä ei ole ollenkaan appia Linuxille, vaan Netflixiä täytyy katsoa verkkoselaimen kautta.

Aloitin tosiaan aluksi Firefoxin parissa. 

Ensin latasin itselleni kokonaan uuden Ubuntu -palvelimen, jotta saan aloitettua puhtaalla pöydällä. Latasin myöskin palvelimelle Saltstackin, jotta moduulin teko onnistuu. Tarkastin vielä, että minion oli hereillä ja toimii.

<img width="256" alt="image" src="https://user-images.githubusercontent.com/118457367/206497242-609821e4-4c47-4f44-86d5-054e049445a8.png">

Ensimmäisenä latailin tuon Firefoxin masterille, josta tarkoitus lähteä niitä asentelemaan minionille. 

Ensimmäisenä Firefoxin lataus itselleni. ELi asensin sitä itselleni tuolla:

```sudo apt install firefox```

Loin aluksi skriptin (joka kertoi että olet lataamassa Firefoxia ja lataaa sen), jonka testasin että toimii ja lisäsin minionille (state.apply). Sitten heräsin siihen, etten saa ubtuntu serverillä auki sitä nettisivua, joten päätin ladata ubuntu desktopin asioiden helpottamiseksi. Jatkuu huomenna 8.12.

Homma tosiaan jatkui vasta 14.12, joten nyt yritetään uudelleen. Ensin latailin sen Ubuntu desktopin (https://ubuntu.com/download/desktop). 








