1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)


# database intro library
- Ci sono clienti che effettuano ordini.
  Un ordine può contenere più prodotti e viene preparato da un dipendente.
  Un ordine ha associato uno o più pagamenti (considerando eventuali tentativi falliti)       

## data types:
- strings: [ varchar(number), char(number), text, longtext ]
- number: [ tinyint, small/medium int, int, int, bigint ]
- decimals: [ float(i,d), double(i,d), decimal(i,d) ]
- dates: [ DATETIME, DATE, YEAR, TIME, TIMESTRAP ]

## data attributes:
- PK -> primary key
- AI -> auto increment
- NN -> NOT NULL
- UNIQUE 

## dipartimenti:
- id_dipartimento   | PK
- nome

## corsi di laurea:
- id_corso_laurea   | PK
- id_dipartimento   | FK
- nome 
- crediti

## corsi:
- id_corso          | PK
- id_corso_laurea   | FK
- id_cfu?               
- nome

## insegnanti:
- id_insegnante     | PK
- nome
- cognome
- email
- password

## esami:
- id_esame          | PK
- id_corso          | FK
- id_insegnante     | FK             
- id_cfu? 
- voto
- crediti
- data

## studenti:
- id_studente       | PK
- id_corso_laurea   | FK
- id_voto           | FK
- nome
- cognome
- email
- password

## iscrizioni:
- id_iscrizione     | PK
- id_studente       | FK
- id_esame          | FK

## voti:
- id_voto           | PK
- id_iscrizione     | FK












