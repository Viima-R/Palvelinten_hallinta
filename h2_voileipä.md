## x) Lue ja tiivistä

Viikko 14 kotitehtävät

### Karvinen 2026: Sudo without password
- Salasanan kirjoittaminen sudo komentoja ajettaessa orja koneelle on turhauttavaa ja aikavievää.
- Ohjeet sudon käyttöön ilman että salasanaa tarvitsee aina antaa.
  - Käyttäjän ja ryhmän luominen
  - Root shell auki toiseen ikkunaan, jos jotain menee rikki, voidaan mahdollisesti korjata sitä kautta.
  - Lisätään sääntö käyttäjä/ryhmä oikeuksiin lumoamalle ryhmälle, jossa käyttäjä on, joka sallii salasanattoman sudon käytön
- **Testaus!**
Miksi tätä ei voisi tehdä suoraan root shellissä jos siellä pystyisi sen myös korjaamaan jos jotain menee rikki?

### Karvinen 2026: Passwordless Sudo with Ansible
  - Tehdään ansiblella automatisoiden mitä opittiin aikaisemmassa artikkelissa.
  - On hyvä ymmärtää ja osata tehdä manuaalisesti ennen kun alkaa automatisoimaan.

### ansible-doc

  #### Copy
  Kopio tiedoston tai polkurakenteen, joko master koneelta tai etäkoneelta, annettuun sijaintiin etäkoneella.

  <img width="410" height="139" alt="Image" src="https://github.com/user-attachments/assets/93dbb4a0-bc46-46e8-97de-e237d6bb9e99" />

  Esimerkki tiedoston kopioimisesta ja omistajan ja oikeuksien asettamisesta.

  #### Apt
  Hallinoi apt paketteja

  <img width="318" height="93" alt="Image" src="https://github.com/user-attachments/assets/77d558a9-4b9d-448c-902a-2259b49e8872" />

  Esimerkki useamman paketin asentamisesta.

  #### file
  Antaa atribuutteja tai vaihtoehtoisesti poistaa tiedostoja, kansioita tai symlinkkejä.

  <img width="309" height="80" alt="Image" src="https://github.com/user-attachments/assets/80bb681a-abd5-4ace-a062-81c0dc0caf28" />

  Esimerkki tiedoston poistamisesta.
  
  #### user
  Hallinoi käyttäjiä.

  <img width="466" height="77" alt="Image" src="https://github.com/user-attachments/assets/f272ae8c-29c8-414f-a234-c7a0228c1229" />

  Esimerkki luo käyttäjän johnd ja sille kotihakemiston.

  #### authorized_key
  Lisää tai poistaa sallitun SSH avaimen tietyltä käyttäjältä
  
  ##### key
  Avain, joko merkkijonona tai linkkinä

  ##### user
  Käyttäjä tai etälaite, jonka avainta tiedostoa muokataan
  
  <img width="391" height="102" alt="Image" src="https://github.com/user-attachments/assets/2bf1439a-1a0a-4222-959a-17e52f07dc71" />

  Esimerkki miten annetaan käyttäjälle avain käyttämällä linkkiä github reposta.

  ## a) Sudoless
