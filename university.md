# Table name: university
- id: PK BIGINT AI NOT NULL UNIQUE 
- dipartimenti
- corsi di laurea
- corsi
- insegnanti
- appelli d'esame
- voti




# Table name: dipartimenti
- id: PK BIGINT AI NOT NULL UNIQUE 
- title:

## Table name: corsi di laurea
- id: PK BIGINT AI NOT NULL UNIQUE 
- dipartimento ID:
- title:

## Table name: corsi
- id: PK BIGINT AI NOT NULL UNIQUE 
- corso di laurea ID (FK)
- title: 
- hours:
- credits:

## Table name: appelli d'esame
- id: PK BIGINT AI NOT NULL UNIQUE 
- studente ID
- corso ID (FK)
- session date:
- score:

## Table name: insegnanti
- id: PK BIGINT AI NOT NULL UNIQUE 
- corso ID(FK)
- name:
- surname:
- email:
- matricola:

## Table name: studenti
- id: PK BIGINT AI NOT NULL UNIQUE 
- name:
- surname:
- date of birth:
- phone numb:
- email:
- matricola:

## Table name: esami
- id: PK BIGINT AI NOT NULL UNIQUE 
- title:

## table name: voti
- id: PK BIGINT AI NOT NULL UNIQUE 
- studente ID: (FK)
- appello d'esame ID: (FK)
- score


