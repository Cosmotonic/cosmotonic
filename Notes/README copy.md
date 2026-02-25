# Lokalt udvikling
Vagrant opretter en VM med samme miljø for alle udviklere.  
Docker kører oven på Vagrant og starter applikationen.

**Rækkefølge:**
1. `vagrant up` – starter VM'en
2. `vagrant ssh` – logger ind på VM'en
3. `docker-compose up` – starter applikationen

Applikationen kører lokalt så du kan se hvad du udvikler.

# Produktion
Digital Ocean er serveren. Docker deployer og kører applikationen der.

# Pointen
Vagrant sikrer alle udviklere arbejder under samme betingelser lokalt.  
Docker sikrer applikationen kører ens lokalt og i produktion.


# Project Commands                                  - Description
ssh -i ~/.ssh/id_ed25519 root@167.172.185.218       Enter server
ctrl + æ                                            skift til terminal


# LINUX Commands 
## Navigation
- `pwd` – vis hvor du er
- `ls` – vis filer i mappe
- `ls -la` – vis alt inkl. skjulte filer
- `cd <mappe>` – gå ind i mappe
- `cd ..` – gå et niveau op
- `cd ~` – gå til rod-mappen

## Filer
- `cat <fil>` – vis indhold af fil
- `nano <fil>` – rediger fil
- `cp <fra> <til>` – kopier fil
- `mv <fra> <til>` – flyt/omdøb fil
- `rm <fil>` – slet fil
- `mkdir <mappe>` – opret mappe
    
## System
- `whoami` – vis hvem du er logget ind som
- `who` – vis hvem der er logget ind
- `htop` – vis ressourceforbrug
- `df -h` – vis diskplads
- `free -h` – vis RAM forbrug

## Docker
- `docker ps` – vis kørende containers
- `docker ps -a` – vis alle containers
- `docker-compose up -d` – start applikation i baggrunden
- `docker-compose down` – stop applikation
- `docker logs <container>` – vis logs fra container

## Netværk
- `curl <url>` – lav HTTP request
- `ping <ip>` – test forbindelse

## Pakker
- `apt install <pakke> -y` – installer pakke
- `apt update` – opdater pakkeliste


# SQLite Commands

## Åbn database
```bash
sqlite3 minitwit-java.db          # åbn database
```

## Dot commands (SQLite shell)
- `.tables` – vis alle tabeller
- `.schema <tabel>` – vis kolonner og typer for en tabel
- `.headers on` – vis kolonnenavne i output
- `.mode column` – pænt formateret output
- `.mode json` – output som JSON
- `.mode csv` – output som CSV
- `.databases` – vis hvilken .db fil du er tilsluttet
- `.quit` – afslut SQLite shell

## Gem output til fil
```sql
.output /sti/til/output.csv
SELECT * FROM user;
.output stdout   -- skift tilbage til terminal
```

## Eller direkte fra shell (uden at gå ind i SQLite)
```bash
sqlite3 -json minitwit-java.db "SELECT * FROM user;" > output.json
sqlite3 -csv minitwit-java.db "SELECT * FROM user;" > output.csv
```

## SQL queries
```sql
SELECT * FROM user;                                         -- vis alle rækker
SELECT email FROM user;                                     -- vis specifik kolonne
SELECT * FROM user WHERE email LIKE '%@gmail.com';          -- filtrer på gmail
SELECT * FROM user LIMIT 10;                                -- begræns antal rækker
```

## Tabel operationer
```sql
CREATE TABLE gmail_users AS                                 -- opret ny tabel fra query
    SELECT * FROM user WHERE email LIKE '%@gmail.com';

DROP TABLE gmail_users;                                     -- slet tabel
```