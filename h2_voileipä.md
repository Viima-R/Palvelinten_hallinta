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
  
  Koska tarkoituksena on tehdä sudoton käyttäjä ansiblea varten otin ensin SSH:n localhostiin ja sitten tein käyttäjän viimah2 ja ryhmän sudoton, johon lisäsin käyttäjän viimah2.

  <img width="473" height="292" alt="Image" src="https://github.com/user-attachments/assets/3ef76f93-27a9-4b4a-a3f1-8079c1b91768" />

  Avasin uuden terminaalin ja menin root shelliin, jonka jälkeen palasin toiseen terminaaliin ja tein /etc/sudoers.d kansioon uuden tiedoston sudoton, jossa annoin ryhmälle sudoton oikeudet käyttää sudoa ilman salasanaa.

  Sen jälkeen poistuin SSH:sta ja tein ssh-copy-id viimah2@localhost

  <img width="397" height="87" alt="Image" src="https://github.com/user-attachments/assets/52329cf9-7105-483d-a2bd-ca78b240b2e0" />

  Testasin ottamalla manuaalisesti ssh yhteyden ja ajamalla sudo komennon ja toimi ilman sudoa!

  <img width="425" height="257" alt="Image" src="https://github.com/user-attachments/assets/bf9873fc-5c43-4711-bc0d-ffbca52e827c" />

  Jonka jälkeen testasin saman vielä ansiblella, lisäämällä become: true site.yml tiedostoon, mikä myöskin toimi!

  <img width="1125" height="644" alt="Image" src="https://github.com/user-attachments/assets/34ba59c2-189a-4854-8868-ad4b5651f885" />

  ## b) Antero

  Nyt sama kun aikaisemmin mutta kokonaan ansiblella.

  <img width="239" height="202" alt="Image" src="https://github.com/user-attachments/assets/970caade-7ade-4fd8-bfdb-7877eba92caa" />

  ansible.cfg on samanlainen kun aikaisemminkin, mutta muut ovat vastaavasti.

  <img width="949" height="616" alt="Image" src="https://github.com/user-attachments/assets/f32fa8c8-a7a3-476b-b951-2b2d8e5357c1" />

  Olin vähän epävarma, että kun tuo käyttäjä luodaan ja sillä käyttäjällä halutaan ajaa tuo toinen rooli, joka ei sitten enää vaadi salasanaa, niin lisäsin hostiin tuon localhost käyttäjän, jolla tehtiin ensin toi       harkka2b käyttäjä jolta sitten oikeudet löytyy. Mutta tähän olisi varmaan ollut jokin parempi tapa koska nyt se herjaa jatkuvasti sitä localhostia siellä, kai sen vois jälkeenpäin poistaa mutta en keksinyt parempaa tapaa?

  <img width="1165" height="525" alt="Image" src="https://github.com/user-attachments/assets/6503995d-dc7c-43ca-bad6-8103d154556f" />

  
