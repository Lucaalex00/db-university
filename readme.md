Esercizio di oggi:

nome repo: db-university

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Table names

## departements
id | BIGINT | UNIQUE | AI | PK | NOTNULL | INDEX
name | VARCHAR(50) | NOTNULL | 
?head

 <!-- corso di laurea -->
## courses 
id | BIGINT | UNIQUE | AI | FK | NOTNULL | INDEX
name | VARCHAR(255) | NOTNULL
description | TEXT | NULL
closed_enrollment | TINYINT | NOTNULL
partecipants | SMALLINT | NULL
cfu | TINYINT | NOTNULL
years | TINYINT | NOTNULL


<!-- materia del corso -->
## subjects
id | BIGINT | UNIQUE | AI | FK | NOTNULL | INDEX
name | VARCHAR(255) | NOTNULL
description | TEXT | NULL
presence | TINYINT | NOTNULL
cfu | TINYINT | NOTNULL

## teachers
id | BIGINT | UNIQUE | AI | FK | NOTNULL | INDEX
full_name | VARCHAR(150) | NOTNULL
age | DATE | NULL
salary | FLOAT(8,2) | NULL
class | VARCHAR(255) | NOTNULL
role | VARCHAR(30) | NULL 
mail | VARCHAR(50) | NOTNULL | UNIQUE
image | VARCHAR(255) | NULL | DEFAULT(https://lorempicsum.jpg)

## students
id | BIGINT | UNIQUE | AI | FK | NOTNULL | INDEX
full_name | VARCHAR(150) | NOTNULL
age | DATE | NULL
identification_number | BIGINT | UNIQUE | NOTNULL
mail | mail | VARCHAR(50) | NOTNULL | UNIQUE
image | VARCHAR(255) | NULL | DEFAULT(https://lorempicsum.jpg)
cours | VARCHAR(255) | NOTNULL
submit_year | TINYINT | NOTNULL
payment_status | VARCHAR(50) | NOTNULL
less_able | TINYINT | NOTNULL
notes | TEXT | NULL
cfu | TINYINT | NOTNULL

## exams
id | BIGINT | UNIQUE | AI | FK | NOTNULL | INDEX
method | VARCHAR(50) | NOTNULL
date | DATETIME | NOTNULL
session | VARCHAR(35) | NULL
professor_presence | TINYINT | NOTNULL
