# x) Lue ja tiivistä

- Git on versionhallinta järjestelmä, joka varastoi tilannekaappauksia tiedostoista ja näitä kaappauksia vertaamalla voidaan tarkastella muutoksia tiedostoissa.
- Toiminta enimmäkseen paikallista, joka takaa nopean käyttökokemuksen.
- Tietojen eheyden varmistamiseen käytetään SHA-1 tarkistussumma
- Kolme päätilaa modified: tiedostoja muokattu, staged: muokatut tiedostot valittu seuraavaan committiin ja commited: tiedot varastoitu, eli niistä on tehty tilannekaappaus.

  ```
  git add .
  ```
  Tämä komento valitsee kaikki muokatut tiedostot commitoitaviksi (pisteen sijasta voi käyttää "--all" tai kirjoitta tiedostojen nimet/polut). (docs/git-add)

  ```
  git commit
  ```

  Tallentaa muutokset git-historiaan, yhteydessä annetaan kommentti kuvaamaan muutoksia. (docs/git-commit)

  ```
  git pull
  ```

  Hakee muutokset etä-varastosta (remote repository) ja päivittää paikalliset tiedostot haetuilla muutoksilla. (docs/git-pull)

  ```
  git push
  ```

  Vie tekemäsi muutokset etä-varastoon ja päivittää tiedostot siellä muutoksillasi. (docs/git-push)

  # a) Online

  Github repositoryn tekeminen, ensin menin osoitteeseen:

  ```
  https://github.com/new
  ```

  Jossa tein seuraavat valinnat:

  <img width="774" height="669" alt="Image" src="https://github.com/user-attachments/assets/aece4969-e05a-4c5d-b9dc-3e49c32311c4" />

  Description kohdassa täytetty kirjoittuu README.md tiedostoon.

  Repo näyttää siis tältä:

  <img width="945" height="483" alt="kuva" src="https://github.com/user-attachments/assets/8d35fe13-4fc8-45ae-82f1-2df7c045e909" />


  # b) Dolly

  Kloonataan repo koneelleni, ensin otin linkin, jota käytän kloonaamiseen.

  <img width="405" height="340" alt="kuva" src="https://github.com/user-attachments/assets/d27cc31b-4124-4c3b-95de-22085f79d0c9" />

  Syötin git clone komennon linkin kanssa.

  <img width="519" height="121" alt="kuva" src="https://github.com/user-attachments/assets/5dd274c5-5fdb-41b8-872d-b29a6195f41f" />

  Muutin README.md tiedoston sisältöä.

  <img width="791" height="176" alt="kuva" src="https://github.com/user-attachments/assets/2fb955a7-9f00-40f6-b1c0-b4909728e852" />

  Ja ajoin git komennot muutosten viemiseksi repoon, käytin "git status" näyttääkseni muutetun tiedoston.

  <img width="604" height="529" alt="kuva" src="https://github.com/user-attachments/assets/65461a40-12a3-445c-abd8-ffaa4fa02c2e" />

  Muutokset ilmeistyivät repoon!

  <img width="918" height="562" alt="kuva" src="https://github.com/user-attachments/assets/648cfd09-f3b9-4688-8b18-f649a0046a2b" />

  # c) Doh!

  Tehdään tyhmä muutos README.md tiedostoon, kuten vaikka poistetaan kaikki teksti.

  <img width="751" height="132" alt="kuva" src="https://github.com/user-attachments/assets/69abb5a1-8d4b-429c-b3e7-6c6fa0e1b46e" />

  "git status" komennolla näytän, että tiedostoon on tehty muutoksia.

  <img width="612" height="182" alt="kuva" src="https://github.com/user-attachments/assets/081df73b-1c15-42aa-b689-3b7420186dff" />

  Kumotaan muutokset "git reset --hard" komennolla, ja näytetään tilanne status komennolla.

  <img width="610" height="213" alt="kuva" src="https://github.com/user-attachments/assets/3b811e93-5d47-4440-b9fb-33ce0c32c73e" />

  Sekä tarkistetaan README.md

  <img width="786" height="174" alt="kuva" src="https://github.com/user-attachments/assets/3f8e7d4f-9685-4a31-82f2-ab73c188f37e" />

  Tyhmä muutos on kumoutunut!

  # d) Tukki

  Tarkastellaan lokia komennolla "git log"

  <img width="611" height="190" alt="kuva" src="https://github.com/user-attachments/assets/cea5a42e-04d5-43b7-a619-fa76bac01e4b" />

  Ensimmäinen tapahtuma on kun repo luotiin, kommenttina siinä on "Initial commit". Toisena tapahtumana on b kohdassa tehty muutokset README.md tiedostoon, jossa kommenttina "Modified README.md".

  # e) Gitanbile

  Avasin virtuaalikoneen ja kloonasin repon sinne.

  <img width="719" height="132" alt="kuva" src="https://github.com/user-attachments/assets/a80bd761-bdba-4403-9e73-6e0424319d1a" />

  Tein yksinkertaisen "hello_world" ansible kansion repon sisään.

  <img width="737" height="707" alt="kuva" src="https://github.com/user-attachments/assets/0729529e-6d15-41ab-b934-04f81f494bde" />

  Ajoin playbookin toimivuuden varmistamiseksi.

  <img width="763" height="260" alt="kuva" src="https://github.com/user-attachments/assets/039334f2-2bc3-421b-8436-29b2bd13b7e1" />

  Lisätään se versionhallintaan eli commitoidaan.

  <img width="761" height="309" alt="kuva" src="https://github.com/user-attachments/assets/c6a7cf5e-2d2c-4270-945a-a998eafed2c1" />

  Tehdään jokin muutos, muokataan tekstiä "main.yml" tiedostossa.

  <img width="762" height="360" alt="kuva" src="https://github.com/user-attachments/assets/72243c69-0804-4b72-94c5-9e8b2e1dade0" />

  Ja sitten "git add" ja "git commit"

  <img width="762" height="310" alt="kuva" src="https://github.com/user-attachments/assets/1e2d3bee-e3b1-4b3c-9164-4289b7b3cd3b" />

  Työnnetään nyt viellä Github repoon, eli "git pull" jotta ollaan ajantasalla jos joku muu olisi tehnyt muutoksia ja sitten "git push".

  <img width="575" height="223" alt="kuva" src="https://github.com/user-attachments/assets/cf853800-79a8-49e0-9d84-38808ae1ff1b" />

  Ja näkyy githubissa.

  <img width="914" height="316" alt="kuva" src="https://github.com/user-attachments/assets/e40f71f5-7343-40a4-8c55-6e61e779b6ed" />

  # f) Hae pari projektiin Moodlen keskustelusta

  Tehty!

  # g) Vapaaehtoinen

  Tää tässä tehdessä tulikin vähän tehtyä kun tein aluksi windowsilla ja sitten virtuaalikoneella debianilla toi e kohta. Käytin komentorivinä windowsissa "git bash" ohjelmaa, tällä tekeminen on aikalailla sama kuin     Linuxilla tekisi (komennot on kutakuinkin samata).


# Lähteet

- https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
- https://git-scm.com/docs





  




  







  
