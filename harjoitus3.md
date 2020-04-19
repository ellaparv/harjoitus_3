Tämä on Palvelinten hallinta -kurssin harjoitus numero 3.

Ennen tehtävien aloittamista boottasin live-tikulta Xubuntu 18.04.3 -työpöydän. Käytössäni on Lenovo ideapad 530S tietokone.

#a) MarkDown. Tee tämän tehtävän raportti MarkDownina.
Aloin tekemään tehtävää klo 13:20.
Aloitin tehtävän luomalla osoitteessa https://github.com/ uuden repositoryn klikkaamalla new, asettamalla repositorylle nimen,asetuksiksi public ja "initialize this repository with a README"
Valitsemalla tämän, github luo valmiiksi README.md -tiedoston. Tämän jälkeen "create repository".
Tämän jälkeen klikkasin luomassani kansiossa clone or download ja kopioin linkin.
Sitten siirryin terminaaliin. Ensin asensin gitin:
    sudo apt-get install git -y 
ja kopioin luomani kansion komennolla:
    git clone https://github.com/ellaparv/harjoitus_3.git
Nyt pystyn käyttämään kansiota myös komentoriviltä käsin. Loin harjoitus_3 kansioon tiedoston tämän tämän tehtävän kirjoittamista varten komennolla
    nano harjoitus3.md.

Luotuani tiedoston laitoin
komennon
    git add. && git commit
jotta tekemäni muutokset tallentuvat. Tämä komento tulee laittaa aina muutoksien tekemisen jälkeen. Sitten määrittelin sähköpostin ja käyttäjän:
    git config --global user.email "user@example.com"
    git config --global user.name "Etunimi Sukunimi".
Tekemiäni muutoksia pystyi tarkastelemaan komennolla
    git log --patch

#d) Näytä omalla git-varastollasi esimerkit komennoista 'git log', 'git diff' ja 'git blame'. Selitä tulokset.

Ensimmäiseksi kokeilin komentoa
     git log
, joka näytti tekemäni tiedostot ja niiden omistajat sekä kellonajat.:

commit 103d0abb0ab0d7ec5b537c02a0780c6b99f65540 (HEAD -> master, origin/master, origin/HEAD)
Author: Ella Parviainen <ella.parviainen@myy.haaga-helia.fi>
Date:   Sun Apr 19 10:43:07 2020 +0000

Modified harjoitus3.md

commit 70cb6b8424e45f15ddb6016d9c00b9bfa9079f60
Author: Ella Parviainen <ella.parviainen@myy.haaga-helia.fi>
Date:   Sun Apr 19 10:38:38 2020 +0000

Add purpose to harjoitus3

commit 607e3e913fa846804f6eb86fa7118adfe9fcac26
Author: ellaparv <60319002+ellaparv@users.noreply.github.com>
Date:   Sun Apr 19 10:16:28 2020 +0000

Initial commit


Seuraavaksi
    git diff
joka näytti poistetut (-)  ja lisätyt (+) rivit tiedostossa harjoitus3.md.


Viimeisenä
    git blame
joka näytti vain mahdollisia vipuja, mitä voi käyttää komennon yhteydessä.
Etsin lisää tietoa git blamesta, ja sivulla https://git-scm.com/docs/git-blame kerrottiin, että blame näyttää kuka omistaja on tehnyt minkäkin muutoksen milläkin rivillä. 
Laitoin komennon
    git blame harjoitus3.md
ja nyt näytölle ilmestyi listaus tekemistäni muutoksista kappaleittain:

70cb6b84 (Ella Parviainen 2020-04-19 10:38:38 +0000  1) Tämä on Palvelinten hallinta -kurssin harjoitus numero 3.
70cb6b84 (Ella Parviainen 2020-04-19 10:38:38 +0000  2) 

#e) Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset 'git reset -hard'.
Ennen muutoksen tekemistä, tallensin tähän mennessä tekemäni muutokset komennolla
    git add . && git commit
jonka jälkeen vielä
    git pull && git push
eli päivitin tiedoston myös palvelimelle.

Sitten tein kansiooni uuden tiedoston
    nano tyhma.md
ja lisäsin sinne tekstiä. Sitten annoin komennon
    git add .
ja katsoin komennolla ls, että luomani tiedosto todella oli kansiossa. Oli se.
Sitten annoin komennon
    git reset --hard
jolloin tuli ilmoitus
HEAD is now at f154a6f Modified harjoitus3.md
eli tiedostot olivat siinä tilassa, milloin olin ne viime kerran tallentanut.

 
#f) Tee uusi salt-moduuli.

Asensin salt-masterin ja salt-minionin samalle koneelle.
Käytin apuna tätä aiemmin tekemääni ohjetta: https://ellaparviainen.wordpress.com/2020/04/07/palvelinten-hallinta-salt-ja-idempotenssi/

    sudo apt-get install salt-master -y
    hostname -I
    sudo apt-get update
    sudo apt-get install -y salt-minion

Sitten muokkasin tiedostoa
    sudoedit /etc/salt/minion
kohtaan master tuli aiemmin katsomani IP-osoite ja kohtaan id orjan nimi.

Seuraavaksi salt-minion uudelleen käyntiin
    sudo systemctl restart salt-minion.service
ja
    sudo salt-key -A
eli aktivoidaan avain. Jatketaan vielä y eteenpäin jolloin minion on aktivoitu masterille.
Testasin, vastaako minion komennolla
    sudo salt 'ella' cmd.run 'whoami'
jolloin sain vastauksen
ella:root.

Päätin asentaa ohjelman neofetch, joka on sys tietojen keräämiseen tarkoitettu ohjelma.

    sudo apt-get install neofetch -y

Sitten etsin konfigurointitiedoston. Se löytyi kansiosta /etc/neofetch ja sen nimi oli config.conf.
Avasin ohjelman Neofetch, toimi.
Seuraavaksi siirsin neofetch-asennustiedoston saltin kansioon komennolla
    sudo mv /etc/neofetch /srv/salt/
ja seuraavaksi katsoin, että tiedosto varmasti oli kansiossa srv/salt komennolla ls.
Sitten poistin asentamani ohjelman
    sudo apt-get purge -y neofetch
Seuraavaksi loin tiedoston
    sudoedit init.sls
Jonne tuli sisälle seuraavaa:

neofetch:
  pkg.installed

/etc/neofetch/config.conf:
  file.managed:
    - source: salt://neofetch/config.conf

startneofetch:
  service.running:
    - name: neofetch
    - watch:
      - file: /etc/neofetch/config.conf


Sitten aktivoin tilan komennolla 
    sudo salt 'ella' state.apply neofetch
jolloin hetken odottelun jälkeen tuli näytölle näkyviin tilaan tekemäni muutokset.

pkg.installed toimi, sekä file.managed, mutta service.running kohdalla oli False ja teksti "Unit neofetch.service not found".

En löytänyt tietoa virheilmoituksesta etsinnästä huolimatta.

Lopetin tehtävän klo 16:05. (Kesto 2h 45min)

Lähteet:
Tero Karvinen 2020 Palvelinten hallinta -luennot
http://terokarvinen.com/2016/publish-your-project-with-github
https://ellaparviainen.wordpress.com/2020/04/07/palvelinten-hallinta-salt-ja-idempotenssi/
