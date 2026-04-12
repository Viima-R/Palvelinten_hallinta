# x) Lue ja tiivistä

## Karvinen 2026: Apache installed with Ansible - quick notes
- Esimerkki apachen asennukseen, verkkosivun luomiseen ja konfiguroimiseen ansiblella.

## Ansible Community Documentation: Handlers: running operations on change
- Handlers on hyvä silloin kun haluaa ajaa taskin vain sillon kun se tekisi muutoksia systeemiin.
- Notify on osa handlersin toimintaa, kun luot handlerin voit nimetä sen ja kun luot muita tehtäviä voit nimen avulla huomauttaa(notify), että handler tarkistus tehdään.

## 'ansible-doc service':
- Hallinnoi palveluita orja koneilla, voit esim. sammuttaa, käynnistää ja uudelleenkäynnistää demoneita.
 - Enabled komennolla voi määritellä jonkin palvelun käynnistymään bootin yhteydessä.
 - Name määrittelee palvelun, mitä hallinoidaan.
 - Statella voidaan määritellä haluttu palvelun tila, jos halutaan että demoni on käynnissä voidaan käyttää "started" ja se käynnistää demonin jos se ei ole käynnissä ja jos on se ei tee mitään.
 - Esimerkissä pystäytetään palvelu httpd, jos se on käynnissä.

<img width="370" height="84" alt="Image" src="https://github.com/user-attachments/assets/b22e70e3-81d5-4d54-b202-ab6fbc8c3cb6" />
 

# a) Apassi
Ensin pysäytin nginx:än, joka mulla oli päällä tunnilla harjoittelusta ja asensin Apachen.

<img width="417" height="76" alt="Image" src="https://github.com/user-attachments/assets/af3b3ecf-b6da-4198-97e5-534190a5ae8a" />

Apache oli automaattisesti päällä heti asennuksen jälkeen ja pystyin jo näkemään apachen default sivun localhostissa.

<img width="893" height="329" alt="Image" src="https://github.com/user-attachments/assets/516ca5e4-504d-43fe-8dd2-9815a6899881" />

Tein kotihakemistooni uuden hakemiston harkka3sivu ja loin sen sisään html tiedoston.

<img width="440" height="314" alt="Image" src="https://github.com/user-attachments/assets/fb72ecf5-6365-4795-ae09-4942e4777f7a" />

Tämän jälkeen menin /etc/apache2/sites-available ja otin mallia tiedostosta "000-default.conf" mallia, miten konffaus kuuluu tehdä, ja tein oman tiedoston samaan sijaintiin.

<img width="575" height="273" alt="Image" src="https://github.com/user-attachments/assets/8128ad9a-0ceb-4d6a-ae06-3ef2cd6eff9d" />

Tämän jälkeen loin linkin luodusta tiedostostamme sijaintiin sites-enabled apache2 kansiossa, sekä uudelleenkäynnistin Apache demonin.

<img width="732" height="35" alt="Image" src="https://github.com/user-attachments/assets/8b520c30-0412-47c7-88f6-2edf574792ea" />

Ajattelin, että tämän jälkeen localhosti näyttäisi jonkin näköistä erroria koska hakemistolle ei ole annettu vielä oikeuksia mutta default sivu näkyi viellä localhostissa. Hetken ihmettelemisen jälkeen huomasin, että koti.conf tiedostossa
olin antanu tiedoston root sijainniksi kun sen pitäisi olla sen hakemisto, korjasin ja uudelleenkäynnistin Apache demonin. Vaihdoin myös html tiedoston nimeksi index.html.
Tästäkin huolimatta localhost näytti vielä default sivun. Tässä kohtaa mietin, että ehkä se on kumminkin pääsy oikeuksista vaikka sivu ei sitä herjaa ja kokeilin antaa oikeudet kotihakemistooni, sivun hakemistoon ja html tiedostoon.

<img width="681" height="62" alt="Image" src="https://github.com/user-attachments/assets/be43c904-1985-4ba5-93bc-87a508801896" />

Sivu pysyi kuitenkin muuttumattomana, joten olin missannu jotain muuta. Kävin läpi kohta kohdalta, mitä olin tehnyt ja en keksinyt, mikä voisi olla muuten kuin, että 000-default.conf tiedosto yliajaa tekemäni tiedoston, joten kommentoin kaiken tekstin tiedoston sisällä.
Jälleen kerran käynnistin demonin uudestaan. Tällä kertaa sain ilmoituksen, mitä aikaisemmin olin toivonut "403 Forbidden" eli oletettavasti antamani oikeudet eivät olleet tarpeeksi.

<img width="481" height="274" alt="Image" src="https://github.com/user-attachments/assets/a2005636-4081-48cd-893f-f344086625d0" />

Kävin kuitenkin oikeudet läpi ja niiden pitäisi olla oikein: hakemistoille o+x ja tiedostolle olin jopa antanu liikaa oikeuksia joten poistin kirjoitus oikeudet joten sille jäi vain muille käyttäjille luku oikeudet.
En keksinyt itse joten hain netistä ja löysin lisäyksen (serverfault, 2011) conf tiedostoon \<directory\> rakenteen joten kokeilin tätä myös itse.

<img width="615" height="359" alt="Image" src="https://github.com/user-attachments/assets/1f27839e-c9d5-4ca0-8ac9-f07fd95bf802" />

Tämä toimi! korjasin vielä tekstin lisäämällä html tiedostoon charsetin UTF-8 niin ääkköset toimii ja tämä muokkaus onnistui ilman sudoa!

# b) Moottorix
Seuraavaksi oli saman homman tekeminen nginx:llä eli ensin pysäytin apachen.

<img width="721" height="94" alt="Image" src="https://github.com/user-attachments/assets/2a362cd2-34c2-4b57-9226-9533d27094df" />

Ja käynnistin nginx:n koska se oli jo asennettuna. Poistin myös aikasemmat tekemiseni nginx:n kanssa.

<img width="994" height="319" alt="Image" src="https://github.com/user-attachments/assets/e7a198ce-6b7e-4508-bca8-155dac487e75" />

Aloitin tekemällä /etc/nginx/sites-available kansioon tiedoston "koti" sain tämän tekemiseen esimerkin "default" tiedostosta. Käytin samaa hakemistoa kuin Apache tehtävässä.

<img width="719" height="345" alt="Image" src="https://github.com/user-attachments/assets/8f85b7ce-9ae4-4f87-b3bb-acb4d7cd86a5" />

Ja tein symlinkin tästä tiedostosta sites-enabled kansioon ja uudelleenkäynnistin nginx:n.

<img width="743" height="42" alt="Image" src="https://github.com/user-attachments/assets/b3226d6c-4133-4aea-88b8-e03f5deea0e6" />

Localhost näytti kuitenkin vielä, nginx:n default sivua, joten oletin, että kyseessä on samanlainen ongelma kun Apachen kanssa eli default on ensisijainen. Kävin katosomassa, mitä asetuksia default tiedostossa oli ja kyllä
siellä oli kohta, mikä sanoi "default_server" joten poistin sen ja lisäsin viellä sen omaan koti tiedostoon ja homma lähti toimimaan nginx demonin uudelleenkäynnistyksen jälkeen!

<img width="953" height="690" alt="Image" src="https://github.com/user-attachments/assets/b08b5264-0354-4c37-bbdb-ad198afc0b62" />

# c) Automoottorix

**Anteeksi tämän c kohdan sekavuus minulla kaatui selain kesken tämän osion, joten kuvitus on tehty jälkeenpäin ja selostus on muistista mitä tein.**

Lähdin toteuttamaan, mitä olin tehnyt kohdassa b ansiblea käyttäen. Tein tiedostos hosts.ini, ansible.cfg ja site.yml tiedostot sekä roles kansion.

<img width="442" height="292" alt="Image" src="https://github.com/user-attachments/assets/687003a2-080b-4c39-806a-931e3f025938" />

Sen jälkeen tein handlers kansion ja tiedoston, joka käynnistää nginx:n uudestaan kun handleria huomautetaan. Testasin tätä tekemällä hello world taskin ja huomauttamalla handleria siellä, handleri toimi ja teki, mitä pyydettiin tarkistin tämän vielä kattomalla nginx:n statusken ja se oli käynnistynyt uudelleen. (Kuvan hello world on kommentoitu pois koska olen jo siirtynyt työssä eteenpäin ja menetin kuvat tästä työvaiheesta, minulla oli myös kuva playbookin ajosta, joka näytti toimivuuden)

<img width="549" height="189" alt="Image" src="https://github.com/user-attachments/assets/b1269d6a-a55f-457f-a23a-8fe05db6b063" />

Seuraavaksi tein "files" kansion jonka sisään kopioin tiedostot /etc/nginx/sites-available/koti (jonka muokkasin uudella rootilla), /etc/nginx/sites-available/default ja /home/viima/harkka3sivu/index.html kopioin nämä tiedostot, koti määrittelee kotihakemistossa olevan hakemiston kotisivun sijainniksi, defaultia muutin kohdassa b joten muutan sitä tässä ansiblella tehdessäkin ja index.html on sivu, jonka orja kone saa kotisivukseen. Muokkasin index.html kopioimisen jälkeen, jotta se erottuu b osan sivusta.

<img width="348" height="305" alt="Image" src="https://github.com/user-attachments/assets/0f216f16-e57a-443f-8260-552a8497f0ef" />

Tein taskin main.yml tiedostoon seuraavakasi tehtävät: nginx asennus viimeisimpään versioon, koti ja default tiedoston vieminen /etc/nginx/sites-available kansioon, symlinkin luominen tiedostoista sites-enabled kansioon, hakemiston "pubsite" luominen orja koneen käyttäjän "viimaans" kotihakemistoon, oikeiuksien muuttaminen "viimaans" kotihakemistoon, sekä html tiedoston vieminen "pubsite" hakemistoon. Testasin playbookin ja tässä pääsenkin kohtaan, jossa olin kun selaimeni kaatui.

<img width="865" height="288" alt="Image" src="https://github.com/user-attachments/assets/cfa21270-af1c-4071-8abf-7e3b62ddc7b9" />

Kuten kuvasta näkyy kotihakemiston oikeuksien vaihtaminen ei onnistunut koska käyttäjän nimi on kirjoitettu väärin. Korjasin nimen ja ajo onnistui.

<img width="712" height="799" alt="Image" src="https://github.com/user-attachments/assets/80302512-e72e-4c53-bac1-66adb1449f49" />

<img width="878" height="667" alt="Image" src="https://github.com/user-attachments/assets/e64b9815-b6f8-4f37-8597-21643cad6eff" />

Ajo onnistui mutta localhost etusivu ei muuttunut etusivuksi vaikka koti tiedosto, jonka olin kopioinut files kansioon oli muokattu uudella rootilla vaan se näytti vanhaa etusivua. Tarkistin, että onko nginx käynnistynyt uudestaan ja jostain syystä se ei sitä ollut tehnyt. Jostain syystä handleri ei enää toiminut vaikka se toimi hello world testausta ajettaessa. Lisäsin notifyn myös html tiedoston vientiä tekevään tehtävään, sekä laitoin notifyt hipsukoiden sisään, muokkasin html tiedostoa ja ajoin uudeestaan.

Ja nyt toimi!

<img width="1316" height="805" alt="Image" src="https://github.com/user-attachments/assets/a126df52-f25c-4f0a-9684-0f1dce33cc11" />

Lopputilanne:

<img width="317" height="334" alt="kuva" src="https://github.com/user-attachments/assets/08c6405e-0b7d-4b51-9fd3-25137192fde5" />

<img width="475" height="775" alt="kuva" src="https://github.com/user-attachments/assets/26db1c4f-6ed5-4a75-9c73-7b516d4d7225" />



# Lähteet:

- https://terokarvinen.com/apache-ansible/
- https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
- https://serverfault.com/questions/249401/how-to-configure-apache-server-with-localhost-virtual-host


