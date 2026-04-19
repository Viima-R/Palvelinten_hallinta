# x) Lue ja tiivistä

### Karvinen 2023: Configuration Management of Distributed Systems over Unreliable and Hostile Networks 4.12.1, 4.12.2 ja 4.12.3.1

- Infran hallinta ohjelmien täsmäkielet(eli DSL) ovat usein suuria ja saattavat sisältävää satoja funktioita.
- Funktioita ohjataan taustalla eri tavoin eri ohjelmissa.
- Vain osa funktioista näkee raskasta käyttöä, eli vaikka ohjelmat ovat suuria, säännölistä käyttöä näkee vain pieni osa.
- Idempotenssia voidaan toteutaan vertaamalla jo olemassa olevaa ja haluttua tulosta IF lausekkeessa jos ne ovat samat muutosta ei tarvitse tehdä.
- Useimmat konfiguroinnit toteutetaan perus fasiliteeteillä

# a) Räpylä

Valitsin asennettavaksi demoniksi postgresql.

```
sudo apt update
sudo apt upgrade -y
sudo apt install postgresql
```

<img width="639" height="60" alt="Image" src="https://github.com/user-attachments/assets/08c3c151-31b7-431f-9cd7-891c19930598" />
  
# b) Automaatti

Seuraavaksi automatisointi ansiblella.

Tein uuden hakemiston "Harkka4", johon lisäsin ansible.cfg, hosts.ini ja site.yaml tiedostot, sekä roles kansion ja sen alle postgres ja tasks kansiot.

<img width="315" height="361" alt="Image" src="https://github.com/user-attachments/assets/09e19c0c-d70a-4b60-adc0-8f7662bedaa9" />

Jonka jälkeen tein tasks kansioon main.yml tiedoston, jossa postgresql:n uusimman version asennus tapahtuu.

<img width="418" height="94" alt="kuva" src="https://github.com/user-attachments/assets/7bf7b92e-7c1d-4995-9f93-bb8e2a5f7a81" />

Sitten testaamaan, mutta ensin poistin postgressin ja siihen liittyvät paketit.

```
sudo systemctl stop postgresql
sudo apt purge postgresql postgresql-* -y
```

<img width="333" height="33" alt="kuva" src="https://github.com/user-attachments/assets/fbe13cdd-0744-4702-951d-8c9d0bbc8a96" />

Jonka jälkeen ajoin playbookin.

<img width="533" height="229" alt="kuva" src="https://github.com/user-attachments/assets/0512fc3e-eacd-4cdc-871a-9b968ce5cf06" />

Ja varmistin asennuksen onnistuneen.

<img width="335" height="42" alt="kuva" src="https://github.com/user-attachments/assets/bca55fca-2fdf-4382-8b01-46898dfed44f" />

# c) Asetus

<img width="641" height="123" alt="kuva" src="https://github.com/user-attachments/assets/fddfe521-f496-4b88-8e3d-7a28cf170809" />

Kuten kuvasta näkee postgres on oletuksean enabled tilassa, eli se käynnistyy automaattisesti kun palvelin käynnistyy, muutetaan asetusta siten, että se ei käynnisty.

Lisäsin main.yml tiedostoon kohdan joka muutaa postgresql:n disablediksi.

<img width="404" height="203" alt="kuva" src="https://github.com/user-attachments/assets/9b5b20e0-2d93-4096-8b1d-50551e982d5f" />

Ja testasin ajaa playbookin.

<img width="658" height="326" alt="kuva" src="https://github.com/user-attachments/assets/dac3681c-309d-47c2-a752-8e23d81a9893" />

Toimii!

# d) Paikka remonttiin

Poistin postgressin ja siihen liittyvät paketit käyttämällä samoja komentoja kuin käytin kohdassa b.

```
sudo systemctl stop postgresql
sudo apt purge postgresql postgresql-* -y
```

<img width="397" height="83" alt="kuva" src="https://github.com/user-attachments/assets/32b665bc-b577-47e1-8cef-bcbe27b0f7da" />

Ja ajoin playbookin.

<img width="625" height="244" alt="kuva" src="https://github.com/user-attachments/assets/01bf0dde-f063-4099-9612-aa992e534ddc" />

Tarkistin vielä, että postgres ei käynnisty bootin yhteydessä.

<img width="646" height="52" alt="kuva" src="https://github.com/user-attachments/assets/1a844963-a658-4246-aebf-38da8627cebb" />


# e) Idempotentti

Todistaakseen, että tilamme on idempotentti ajoin playbookin vielä pari kertaa uudestaan ja sain, joka kerta seuraavan.

<img width="684" height="241" alt="kuva" src="https://github.com/user-attachments/assets/d5fbadd7-d2e7-4b9b-8361-a7c9e61fc6ff" />

Mitään muutoksia ei siis tapahtunut, koska olimme jo toivotussa tilassa eli tilamme on idempotentti.

# Lähteet
- https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf
- https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/systemd_service_module.html
- https://askubuntu.com/questions/32730/how-to-remove-postgres-from-my-installation










