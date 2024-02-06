Esercizio di oggi: DB UNiversity
nome repo: db-university
Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato (non dovete scompattare il file zip, semplicemente andate nella sezione importa, e fate drag and drop oppure prendetelo dai file delle vostre cartelle, esattamente come visto a lezione), eseguite le query del file allegato.
Cosa consegnare?
Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file txt, md o altro e caricatelo nella vostra repo.
BONUS:
Selezionare nome, descrizione e periodo di tutti i corsi che hanno sito web diverso da null, cfu compresi tra 9 e 12 e che sono del primo anno ed ordinarli in ordine decrescente
P.S. Ad ogni query fatta corrisponde un push.
Buon lavoro.

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


1.
SELECT * 
FROM `students` 
WHERE `date_of_birth`LIKE '1990-%'; 

2.
SELECT * 
FROM `courses` 
WHERE `cfu` >10;

3.
SELECT * 
FROM `students` 
WHERE TIMESTAMPDIFF(YEAR,`date_of_birth`,CURDATE())>=30; 

4.
SELECT * 
FROM `courses` 
WHERE `period` = 'I semestre' 
AND `year` = 1; 

5.
SELECT * 
FROM `exams`
WHERE `date` = '2020/06/20'
AND HOUR(`hour`) >= 14;

6.
SELECT * 
FROM `degrees`
WHERE `level` = 'magistrale';

7.
SELECT COUNT(name)
AS Number_of_Dipartiments
FROM `departments`;

8.
SELECT COUNT(name) 
AS Number_of_TEACHER_WITH_CELLNULL 
FROM `TEACHERS` 
WHERE `phone` is NULL; 

<!-- BONUS:
Selezionare nome, descrizione e periodo di tutti i corsi che hanno sito web diverso da null, cfu compresi tra 9 e 12 e che sono del primo anno ed ordinarli in ordine decrescente -->

SELECT `name`, `description`, `period` 
FROM `courses`
WHERE `website` is not null
AND `year` = 1
AND `cfu`  BETWEEN 9 AND 12 ORDER BY `cfu` DESC;
