# h6 Kulkurin projekti

Tehtävät on tehty windows 11 pro:lla (versio: 22H2, OSbuild: 22621.900, Windows Feature Experience Pack: 1000.22638.1000.0) käyttäen powershellia. Virtual boxin sisällä en pystynyt käyttämään vagranttia. Vagrantilla tuli erroria, kun yritti käynnistä debian/bullseye64. 

# x) Lue ja tiivistä

[Tero Karvinen vagrant revisited](https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/)

    $ sudo apt-get install vagrant virtualbox    
    $ vagrant init debian/bullseye64    
    $ vagrant up
    $ vagrant ssh
    $ vagrant dertroy
    
[Two machines vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/) 

    $ sudo apt-get install vagrant virtualbox
    $ mkdir twohost/; cd twohost/
    
Vagrantfileen kaikki tarvittavat tiedot. Ssh:lla yhteys.

[Salt Quickstart](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/) 

    $ master$ sudo apt-get install salt-master
    $ master$ sudo apt-get install salt-minion
    
 Orjalle pitää kertoa masterin osoite /etc/salt/minion tiedostoon. Masterilla pitää hyväksyä orjan salt avain.
        
        $ sudo salt-key -A

Tämän jälkeen yhteys masterin ja orjan välillä pitäisi toimia. (Voi joutua muuttamaan tulimuurin portti asetuksia.)

## a) Hello Vagrant. Asenna virtuaalikone Vagrantilla.

Asensin vagrantin koneelle heidän kotisivuilta. [Vagrant download](https://developer.hashicorp.com/vagrant/downloads). Annetaan vagrantille tarvittava boxi (=käyttöjärjestelmä, joka halutaan asennettavan) sekä muut komennot, että saadaan yhteys uuteen virtuaalikoneeseen.

    $ init debian/bullseye64  
    $ vagrant up

Tuli erroria, joka todennäköisesti johtuu windowsista. Löysin netistä vastauksen ongelmaan [Vagrant sollutiuon](https://discuss.hashicorp.com/t/not-able-to-install-any-box-in-vagrant-v-2-3-0-the-box-could-not-be-found/44440/2) ja kävin lisäämässä tarvittavan hyväksynnän vagrantfileen.

![Alt text](/h6/h6a1.png)

Tämän jälkeen pelkkä vagrant ssh ei toiminut. Piti lisätä vagrant id perään.

![Alt text](/h6/h6a2.png)

    $ vagrant global-status
    $ vagrant ssh 13ed36f

![Alt text](/h6/h6a3.png)

Nyt yhteys uuteen virtuaalikoneeseen saatiin.

## b) Yksityisverkko. Asenna kaksi virtuaalikonetta samaan verkkoon Vagrantilla. Laita toisen koneen nimeksi "isanta" ja toisen "renki1". Kokeile, että "renki1" saa yhteyden koneeseen "isanta" (esim. ping tai nc). 

    $ vagrant init
    $ notepad vagrantfile
 
Lisätään vagrantfileen tavittavat tiedot [Vagrantfile](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

    $ vagrant up

Otin yhteyden isanta koneeseen ja testasin ping komennolla yhteyden renki1 koneeseen.

    $ vagrant ssh isanta
    $ ping -c 4 192.168.88.102
    
![Alt text](/h6/h6b1.png)

Numero 4 komennossa tarkoittaa kuinka monta ping paketti lähetetään.

## c) Salt master-slave. Toteuta Salt master-slave -arkkitehtuuri verkon yli. Aseta edellisen kohdan kone renki1 orjaksi koneelle isanta.

Kävin asentamassa salt-masterin isanta koneelle ja salt-minionin renki1 koneelle. Renki1 koneelle minionille pitää määritellä masterin osoite ja minionin id. Sekä isanta koneella pitää käydä hyväksymässä minionin salt-key.

    $ vagrant ssh isanta 
    $ sudo apt-get install salt-master
    $ exit
    
Renki1 koneelle salt-minionin asentaminen

    $ vagrant ssh renki1
    $ sudo apt-get install salt-minion
    $ sudoedit /etc/salt/minion
    $ sudo systemctl restart salt-minion
    $ exit
    
Salt-keyn hyväksyminen isanta koneella.   
    
    $ vagrant ssh isanta 
    $ sudo systemctl restart salt-master
    $ sudo salt-key -A
    $ sudo salt '*' grains.items
    
![Alt text](/h6/h6c1.png)
     
Salt yhteys toimii masterin ja minion välillä.

## d) Oma suola. Tee ensimmäinen työversio projektistasi. Miniprojektilla tulee olla jokin tarkoitus, vaikka se olisi keksitty. Projektilla tulee olla sivu (esim. Github, Gitlab...), josta selviää projektin perustiedot. Toiminnallisuutta tulee olla kokeiltu, mutta sen ei tarvitse olla valmis. Valmiit projektit esitellään viimeisellä tapaamiskerralla. Tässä tehtävässä palautettava työversio ei siis ole vielä lopullinen.

[Salt project](https://github.com/Jiikiam/Saltproject)

Lähteet

https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

https://discuss.hashicorp.com/t/not-able-to-install-any-box-in-vagrant-v-2-3-0-the-box-could-not-be-found/44440/2

https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

https://docs.saltproject.io/en/latest/ref/cli/salt-key.html
