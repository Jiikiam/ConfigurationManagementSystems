# h6 Kulkurin projekti

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
