# Reliable UDP Transport

Acest proiect este o implementare de tip transport sigur peste UDP, conceputa ca tema de laborator pentru retele de calculatoare. Scopul este sa realizezi un protocol de transfer de date mai fiabil decat UDP-ul clasic, folosind mecanisme de handshake, ACK, retransmisie si gestionarea ferestrelor de transmisie.

## Descriere generala

Repository-ul contine un schelet de aplicatie client-server care simuleaza un protocol de nivel transport peste UDP:

- clientul trimite fisiere catre server
- serverul primeste date si le scrie intr-un fisier local
- protocolul este definit prin header-uri customizate pentru segmente de date si control
- partea de retea este implementata pe socket-uri UDP, iar logica transport este realizata in bibliotecile din folderul `lib/`

Proiectul este structurat in C++ si foloseste un model bazat pe thread-uri pentru sender/receiver.

## Protocol si comportament

Protocolul se bazeaza pe un model de tip UDP cu header personalizat, similar cu un protocol de transport simplificat:

- `poli_tcp_data_hdr` pentru segmente de date
- `poli_tcp_ctrl_hdr` pentru segmente de control
- identificare de conexiune prin `conn_id`
- secventiere cu `seq_num` si confirmari cu `ack_num`
- fereastra de receptie / transmitere pentru controlul fluxului

In stadiul actual, proiectul este un schelet de laborator si contine puncte marcate `TODO`, unde trebuie implementata logica completa a protocolului: handshake, ACK-uri, retransmisie, timeout si gestionarea datelor.

## Cerinte

- compilator C++ (`g++`)
- Unix/Linux-like environment
- socket-uri UDP si suport pentru pthreads

## Build

Pentru a compila proiectul:

```bash
make
```

Pentru a curata fisierele generate:

```bash
make clean
```

## Rulare

### Server

Pornirea serverului simplu:

```bash
./server
```

Serverul poate accepta mai multe conexiuni simultan, de exemplu:

```bash
./server 3
```

### Client

Clientul trimite un fisier catre server:

```bash
./client path/to/file.txt
```

Daca vrei sa introduci o intarziere inainte de transmitere:

```bash
./client path/to/file.txt 5
```

## Observatii importante

- In implementarea actuala, clientul trimite catre IP-ul fix `172.16.0.100` pe portul `8032`.
- Daca rulezi aplicatia intr-un alt mediu de retea, trebuie ajustat IP-ul si portul in `client.cpp` si/sau `server.cpp`.
- Pentru o implementare completa a protocolului robust, trebuie completate logica de `setup_connection`, `wait4connect`, `send_data`, `recv_data`, precum si mecanismele de timeout si retransmisie.

## Scop educational

Acest proiect este util pentru intelegerea modului in care functioneaza protocoalele de transport bazate pe UDP, inclusiv:

- gestionarea conexiunilor
- transmiterea fisierelor peste retea
- controlul erorilor si confirmarii
- retransmisia pachetelor pierdute
- simularea unei conexiuni "reliable" peste un transport nefiabil

