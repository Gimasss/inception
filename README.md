*This project has been created as part of the 42 curriculum by giomastr.*

# Inception

## Description

The goal of this project is to build and undestand how Docker works - we need to create a web structure with containers. For each necessary service - NGINX, WordPress, MariaDB - there is a dedicated container, where the “image”? and instructions are.

The single images build for the services are then “compiled” and handled with DockerCompose.

\[Spiega l’uso di Docker e le sorgenti incluse nel progetto — quali cartelle/file, cosa fa ciascun servizio\]

### Design choices

The VM and Dockers both use Debian 12 (Bookworm), as I preferred using a stable, frequently update and commonly used distribution. As required by the subject, the containers are built within the VM into three separate instances, one of each dedicated to a given task - database, FRONTEND??, internet connection. They all communicate through the network they run onto, as it is defined in the Dockerfile by network: inception.

Virtual Machines vs Docker

Why Docker? In itself, docker is a more flexible and lightweight tool. 

A Virtual Machine is a more structured tool - it requires more drive space on the host machine, as it creates its own memory space, uses its own kernel and its own virtual RAM. This translates in a slower and heavier boot up, but in a more stable and reliable machine to work on - ideal for the development of programs that need a safe environment to be built and tested in.
Docker need less resources overall, as it shares the host machine hardware (?), making it thus faster and more portable.

### Secrets vs Environment Variables

Passwords, as sensitive information, cannot be saved in Env Vars, it would make the system more prone to attacks. 

\[Confronto: perché i secrets sono più sicuri per dati sensibili come password (non visibili in `docker inspect`, non nella history delle immagini), mentre le env vars sono adatte per config non sensibile\]

### Docker Network vs Host Network

\[Confronto: isolamento e sicurezza della rete dedicata Docker vs condivisione diretta dello stack di rete dell’host, perché il progetto vieta `network: host`\]

### Docker Volumes vs Bind Mounts

\[Confronto: i volumi sono gestiti da Docker (portabili, con driver dedicati), i bind mount dipendono dal path esatto dell’host — perché il progetto richiede volumi nominati\]

## Instructions

### Prerequisites

-   A Linux VM with Docker and Docker Compose installed
-   \[altro se serve\]

### Installation & Execution

```bash
git clone <repo-url>
cd Inception
make
```

make co will prompt the Docker build and simplify the usage of all necessary commands to work on the given Dockers. It can be used to clean up the initialised containers and stop the process altogether.
More info will be given in DEV\_DOC.md

### Accessing the site

Add to `/etc/hosts`:
127.0.0.1 [giomastr.42.fr](http://giomastr.42.fr)
Then visit: `https://giomastr.42.fr`

## Resources

[https://docs.docker.com/reference/dockerfile/](https://docs.docker.com/reference/dockerfile/)

https://medium.com/@ShantKhayalian/docker-vs-docker-compose-simple-and-fun-explanation-4811582127f7

[https://therahulsarkar.medium.com/understanding-docker-volumes-a-comprehensive-guide-46339aa9ac53](https://therahulsarkar.medium.com/understanding-docker-volumes-a-comprehensive-guide-46339aa9ac53)

[https://www.freecodecamp.org/italian/news/il-comando-linux-scp-come-trasferire-file-via-ssh-da-remoto-a-locale/](https://www.freecodecamp.org/italian/news/il-comando-linux-scp-come-trasferire-file-via-ssh-da-remoto-a-locale/)

### AI usage

I used Anthropic’s AI services mostly as support to understand how to organize and develop the project, properly visualize the flow. During development, I found it necessary to debug errors that occurred whilst re-booting - some seemed to not behave as expected.
In the latest part of the project, preferred the generate a clear and well build markdown template and a diagram that I embedded in the documentation.

\[Descrivi qui, onestamente, per quali task hai usato l’AI e quali parti del progetto: es. “Ho usato Claude per capire la struttura generale Docker Compose e per debug di errori di configurazione (php-fpm socket vs TCP, inizializzazione MariaDB). Ho scritto/rivisto personalmente ogni Dockerfile e script…” — sii specifico\]

## Features

\[Elenco puntato dei servizi implementati: NGINX+TLS, WordPress+php-fpm, MariaDB, volumi persistenti, rete dedicata, secrets, restart automatico\]