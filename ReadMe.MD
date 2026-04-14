Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi `Dipartimenti` (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni `Dipartimento` offre più `Corsi di Laurea` (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni `Corso` di Laurea prevede diversi `Corsi` (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi `Insegnanti`;
ogni Corso prevede più `appelli d'Esame`;
ogni `Studente` è iscritto ad un solo `Corso di Laurea`;
ogni Studente può iscriversi a più appelli di Esame;
per ogni `appello d'Esame` a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.


## tabelle Dipartimento

- id (int, primary key auto increment)
- nome (varchar(255))
- sede (varchar(255))
- telefono (varchar(20))
- email (varchar(255))
- indirizzo VARCHAR(255)
- citta VARCHAR(100)
- cap VARCHAR(10)


## tabelle corso di lauera
- id (int, primary key auto increment)
- nome (varchar(255))
- durata (int)
- descrizione (text)
- id_dipartimento (int)
- classe (varchar(10))

## tabelle corso
- id (int, primary key auto increment)
- nome (varchar(255))
- cfu (int)
- id_corso_laurea (int)
- descrizione (text)
- anno (int)

## tabelle insegnate
- id (int, primary key auto increment)
- nome (varchar(255))
- cognome (varchar(255))
- email (varchar(255)) unique
- telefono (varchar(20))
- id_dipartimento (int, foreign key)  
- specializzazione (varchar(255))
- data_assunzione (data)
- stipendio (decimal(10,2))
- ruolo (varchar(50))

## tabelle studente
- id (int, primary key auto increment)
- nome (varchar(255))
- cognome (varchar(255))
- email (varchar(255)) unique
- telefono (varchar(20))
- id_corso_laurea (int, foreign key)
- matricola (varchar(20) unique)
- data_iscrizione (data)
- anno_corso (int)
- stato (varchar(20))
- data_nascita (date)
- sesso (varchar(10))

## tabelle appello d'esame
- id (int, primary key auto increment)
- data (date)
- ora (time)
- id_corso (int, foreign key)
- id_insegnante (int, foreign key)
- luogo (varchar(255))
- tipo (varchar(50))

## tabelle iscrizione esame
- id (int, primary key auto increment)
- id_studente (int, foreign key)
- id_appello (int, foreign key)
- voto (int)
- esito (varchar(20))

