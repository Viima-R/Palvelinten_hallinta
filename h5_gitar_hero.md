# x) Lue ja tiivistä

- Git on versionhallinta järjestelmä, joka varastoi tilannekaappauksia tiedostoista ja näitä kaappauksia vertaamalla voidaan tarkastella muutoksia tiedostoissa.
- Toiminta enimmäkseen paikallista, joka takaa nopean käyttökokemuksen.
- Tietojen eheyden varmistamiseen käytetään SHA-1 tarkistussumma
- Kolme päätilaa modified: tiedostoja muokattu, staged: muokatut tiedostot valittu seuraavaan committiin ja commited: tiedot varastoitu, eli niistä on tehty tilannekaappaus.

  ```
  git add .
  ```
  Tämä komento valitsee kaikki muokatut tiedostot commitoitaviksi (pisteen sijasta voi käyttää "--all" tai kirjoitta tiedostojen nimet/polut).

  ```
  git commit
  ```

  Tämä komento tallentaa muutokset git-historiaan, yhteydessä annetaan kommentti kuvaamaan muutoksia.

  ```
  git pull
  ```

  Hakee muutokset etä-varastosta (remote repository) ja päivittää paikalliset tiedostot haetuilla muutoksilla.

  ```
  git push
  ```

  Vie tekemäsi muutokset etä-varastoon ja päivittää tiedostot siellä muutoksillasi.

  # a) Online

  
