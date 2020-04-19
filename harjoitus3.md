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
	komennon git add. && git commit
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
joka näytti vain mahdollisia vipuja, mitä voi käyttää komennon yhteydessä. Päätin kokeilla
	git blame --incremental
Etsin lisää tietoa git blamesta, ja sivulla https://git-scm.com/docs/git-blame kerrottiin, että blame näyttää kuka omistaja on tehnyt minkäkin muutoksen milläkin rivillä. 
