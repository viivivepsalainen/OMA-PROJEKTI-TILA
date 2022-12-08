# OMA-PROJEKTI-TILA
palvelinten hallinta s22, oman tilan/moduulin teko 

Käytössä Asus Zenbook Windows 11 käyttöjärjestelmällä, AMD Ryzen 7 prosessorilla ja 8Gt fyysistä muistia. 

Käytin Oracle VM:n kautta Linuxin ubuntupalvelinta, jotta saan sinne luotua herran ja orjan ja testata onnistuuko. 

Tarkoitus asentaa vanhemman ihmisen arjen helpotusta varten hänelle tarpeellisia sovelluksia saltin avulla. Tässä tapauksessa vanhempi ihminen tahtoo kuunnella Spotifytä, katsella Netflixiä sekä selailla nettiä Firefoxin kautta. Eli nuo kolme asennetaan.

Ensin latasin itselleni kokonaan uuden Ubuntu -palvelimen, jotta saan aloitettua puhtaalla pöydällä. Latasin myöskin palvelimelle Saltstackin, jotta moduulin teko onnistuu. Tarkastin vielä, että minion oli hereillä ja toimii.

<img width="256" alt="image" src="https://user-images.githubusercontent.com/118457367/206497242-609821e4-4c47-4f44-86d5-054e049445a8.png">

Ensimmäisenä latailin tuon Spotifyn, Netflixin ja Firefoxin masterille, josta tarkoitus lähteä niitä asentelemaan minionille. 

Ensimmäisenä Spotifyn lataus itselleni. Aloitin etsimällä netistä tietoa, kuinka se lataillaan Ubuntulle. Parin sivun selauksen jälkeen löytyikin toimivat ohjeet, sillä muilla sivuilla olevat gpg avaimet olivat vanhentuneet. (https://www.linuxcapable.com/how-to-install-spotify-on-ubuntu-22-04-lts/).

Ensin tein tarvittavat asennukset, jotta spotify voidaan ladata ATP-menetelmällä (ATP lataa lukee tekstitiedostot ja muuntaa ne PostScript -formaattiin):

komennolla ```sudo apt install curl libcanberra-gtk-module software-properties-common apt-transport-https gnupg2 ubuntu-keyring -y```. 

Tämän jälkeen toin gpg -avaimen, jotta spotify voidaan ladata turvallisesti:

komennolla ```wget -O- https://download.spotify.com/debian/pubkey_5E3C45D7B312C643.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/spotify.gpg```.



