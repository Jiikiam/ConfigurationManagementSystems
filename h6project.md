# h6 Kulkurin projekti

# x) Lue ja tiivistä

[Tero Karvinen vagrant revisited](https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/)

    $ sudo apt-get -y install vagrant virtualbox
    $ vagrant init debian/bullseye64
    $ vagrant up
    $ vagrant ssh
    $ vagrant dertroy
    
[Two machines vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/) 

    $ sudo apt-get install vagrant virtualbox
    $ mkdir twohost/; cd twohost/
    
-  Vagrantfileen kaikki tarvittavat tiedot. Ssh:lla yhteys.
