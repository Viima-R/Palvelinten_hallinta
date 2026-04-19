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

Sitten testaamaan, mutta ensin poistin postgressin.

```
sudo systemctl stop postgresql
sudo apt purge postgresql
```


