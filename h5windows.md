# Homework 5
Käytössä ubuntu serveri versio 22.04.1 LTS. Tällä koneella on salt-master versio 3004.1. Toisella koneella on käytössä Windows 11, jolle salt-minion 3005.1 on asennettu.
## a) Hello Window Salt! Tee Windowsille SLS-tiedostoon Salt-tila, joka tekee tiedoston nimeltä "suolaikkuna.txt".
Siirryin C levyltä käyttäjäni hakemistoon. Loin salt kansion käyttäjälleni ja salt kansioo suolaikkuna kansion. 

	$ cd .\Users\Jokke\
	$ mkdir temp/srv/salt/suolaikkuna
	
Suolaikkuna kansioon tein init.sls tiedoston notepadilla, jossa luki seuraavasti.

![Alt text](/h5/h5a1.png)

Ajoin tiedoston saltilla

	$ salt-call --file-root=. --local state.apply suolaikkuna
	
![Alt text](/h5/h5a3.png)

![Alt text](/h5/h5a2.png)

### b) Ei vihkoa, ei kynää. Kerää Windows-koneen tekniset tiedot tekstitiedostoon. Vapaaehtoinen bonus: Saatko tiedot tallennettua myös json-muodossa?
Käytetään grains.items salt komentoa keräämään järjestelmän tekniset tiedot.

	$ salt-call --local grains.items > C:\Users\Jokke\temp\tiedot.txt
	
![Alt text](/h5/h5b1.png)

Jos tiedosto halutaan json muodossa voidaan sen tehdä seuraavalla komennolla

	$ salt-call --local grains.items | ConvertTo-Json | out-file C:\Users\Jokke\temp\json.txt
	
![Alt text](/h5/h5b2.png)

### c) Kop kop. Onko TCP-portti auki vai kiinni? Näytä esimerkit portin kokeilusta Linuxilla ja Windowsilla. Näytä kummallakin käyttöjärjestelmällä ainakin yksi avoin ja yksi suljettu portti. (Kokeile tätä vain omaan koneeseesi. Vieraiden koneiden ja verkkojen porttiskannaaminen on kiellettyä. Yksittäisen portin testaavat komennot ovat suositeltavia, esim. nc, tnc)
Kokeilin ubuntu serverillä ja windows 11 portteja 22 ja 993. Ubuntulla yksittäisen portin testaaminen onnistuu komennolla.


	$ nc -vz ip portnumber
	
Windowsilla se onnistuu

	$ tnc -port portnumber
	
![Alt text](/h5/h5c2.png)

![Alt text](/h5/h5c3.png)
































