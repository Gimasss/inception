# User Documentation

## What this stack provides

\[Spiega in parole semplici cosa offre l’infrastruttura: un sito WordPress raggiungibile via HTTPS, con database MariaDB dietro le quinte, il tutto containerizzato — a chi si rivolge (utente finale/amministratore del sito)\]

## Starting and stopping the project

### Start

```bash
make
```

\[Spiega cosa succede: build delle immagini, avvio dei container\]

### Stop

```bash
make stop
```

\[Spiega la differenza tra stop (i dati restano) e altre opzioni\]

### Full reset (⚠️ cancella i dati)

```bash
make fclean
```

\[Avvisa chiaramente che cancella database e file WordPress\]

## Accessing the website

\[Spiega il passaggio /etc/hosts se necessario, poi l’URL: [https://giomastr.42.fr](https://giomastr.42.fr)\]

### Accessing the admin panel

URL: `https://giomastr.42.fr/wp-admin`

\[Spiega chi sono gli utenti disponibili — senza scrivere le password in chiaro qui! Rimanda a “Locating credentials” sotto\]

## Locating and managing credentials

\[Spiega DOVE si trovano le credenziali: cartella quali file contengono cosa (db\_password.txt, db\_root\_password.txt, wp\_admin\_password.txt, wp\_user\_password.txt) — senza scrivere le password reali in questo documento\]

Sensible files need to be uploaded in order for the project to work correctly. You will find a  `secrets/`  folder on the Desktop to transfer from host machine to VM.

### Transferring the secrets folder

To transfer files, I used the `scp` Linux utility (Secure Copy Protocol), through the SSH port.

```
scp <filename> user@hostname:/path/dest/ 
```

\[Spiega come cambiarle se necessario: modificare il file .txt corrispondente e ricostruire con `make re`\]

## Checking that services are running correctly

```bash
docker ps -a
```

It displays all dockers, both active and inactive ones.

```bash
make logs
```

\[Spiega come leggere i log per capire se qualcosa non va\]

### Quick health check

```bash
curl -k -o /dev/null -s -w "%{http_code}\n" https://giomastr.42.fr
```

\[Spiega: risposta 200 = tutto ok\]