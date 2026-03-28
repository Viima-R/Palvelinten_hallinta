# Viikko 13 kotitehtävät

Viikon läksynä tehdä hei maailma ansiblella ja varmistaa osaamista SSH:n kanssa

## x) Lue ja tiivistä

### Karvinen 2026: SSH public key - Login without password

- SSH on ratkaisu turvalliseen kirjautumiseen servereille.
- Julkisella avaimella voi automatisoida kirjautumisia
- Ohjeet alkuun pääsemiseen SSH:lla
  - Asennus
  - Testaus
  - Automatisointi
  - Vianmääritys

### Karvinen 2026: Hello Ansible

- Ansible selitetty
  - Konfirugoinnin hallinta työkalu.
  - Toimii SSH:n välityksellä joten se tarvitaan vain master koneella ja orjilla tarvii olla vain SSH ja Python asennettuna.
- Ohjeet aloittamiseen Ansiblella
  - SSH:n testaus ilman Ansiblea ja sen kanssa.
  - Ansiblen asennus
  - Vinkkejä
  - Roolien luonti
  - Vianmääritys

## a) Sshecrets. Asenna SSH-demoni ja testaa se kirjautumalla SSH:lla.

Alkuun siirsin julkisen avaimen käytöstä poistettuihin ja poistin jo virtuaalikoneelle asennetun ssh:n

remote$ mv -v $HOME/.ssh/authorized_keys $HOME/DISABLED_authorized_keys
$ sudo systemctl stop ssh
$ sudo apt-get purge openssh-server

Jonka jälkeen päivitin paketit, asensin SSH:n ja starttasin sen nyt ja joka bootilla.

$ sudo apt-get update
$ sudo apt-get -y install ssh
$ sudo systemctl enable --now ssh

Testasin ottaa yhtettä localhostiin ja kaikki toimi.

## b) Pubkey. Automatisoi ssh-kirjautuminen julkisella avaimella.

Generoin uuden avaimen ja laitoin sen localhostiin, jotta vältyn jatkossa salasanan kirjoittamiselta.

$ ssh-keygen
$ ssh-copy-id localhost

ja testasin taas ja yhteys pelas, eikä kysyny enää salasanaa.

## c) Hei Ansible. Tee hei maailma ansiblella ja kokeile sitä SSH:n yli.

Ansiblea en poistanut ja asentanut uudelleen joten asensin vain micron, bash-completionin ja treen.
Loin uuden hakemiston "Ansible" ja loin sen sisään tiedoston "Hosts.ini" jonka sisältö on "localhost" ja conffasin myös Teron ohjeen mukaan Python herjauksen pois.
Testasin ja toimi, jonka jälkeen tein conffi tiedoston, jossa määrittelin, että jatkossa käyttää tätä "hosts.ini" tiedostoa jatkossa oletuksena.

Tein yml tiedoston jonka sisään määrittelin roolin "hello", jonka kaikki koneet saavat.
Testasin playbookia ja sain odostusten mukaisen vastauksen. "roolia "hello" ei ole luotu"

Loin kansioita niin, että sain hakemisto polun ~/ansible/**roles/hello/tasks/** jonka sisään loin tiedoston main.yml joka kirjoittaa tiedoston /tmp/hello-ansible, jonka sisältö on "moikkelismoi ansible"

- copy:
    dest: /tmp/hello-ansible
    content: "moikkelismoi ansible!\n"

Testasin ja toimi odotusten mukaisesti tiedosto oli luoto orjan /tmp/ hakemistoon.

Lisäsin vielä conffi tiedostoon, jossa aikaisemmin oli määritelty "hosts.ini" oletus inventaarioksi, asettuksen, joka toistaa aina ansiblen tehdyt toimenpiteet.

Testasin ja nyt näin, mitä ansible oli tehnyt:
TASK [hello : copy dest=/tmp/hello-ansible, content=moikkelismoi ansible!
] *****

d) Vapaaehtoinen bonus, vaikea: kokeile Ansiblella jokin näista asetuksista: paketin asennus, asetustiedosto /etc/ alle, käynnistä jokin demoni, tee uusi käyttäjä. Tarvitset todennäköisesti sudoa, become: true.

Tein playbookin, mikä asentaa curlin uusimman version. Lopputulos näyttää tältä

.
├── ansible.cfg
├── hosts.ini
├── roles
│   └── curl
│       └── tasks
│           └── main.yml
└── site.yml

4 directories, 4 files

anisble.cfg, site.yml ja hosts.ini tiedostot on samanlaiset kun aikaisemmassa vain roolin nimi on muutettu site.yml tiedostossa, roolin nimi "curl"

main.yml sisältö:

- name: Install curl
  apt:
    pkg:
      - curl
    state: latest
  become: true

Ajettiin komennolla

$ ansible-playbook site.yml --ask-become-pass

## Lähteet
- https://terokarvinen.com/hello-ansible/
- https://terokarvinen.com/ssh-public-key-login-without-password/
- https://stackoverflow.com/questions/54944080/installing-multiple-packages-in-ansible
- https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_privilege_escalation.html
