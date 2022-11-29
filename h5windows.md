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
