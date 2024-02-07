Utilizzando lo stesso database di ieri, eseguite le query in allegato. Obbligatoriamente ne dovete fare 3 per il group by e tre per le JOIN.
Caricate un secondo file nella stessa repo di ieri (db-university) con le query di oggi.
Buon lavoro!

<!-- group by -->
1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

<!-- join -->
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

<!-- group by -->
1.
SELECT COUNT(*) AS `numero_iscritti`, YEAR(`enrolment_date`) AS `year`
FROM `students`
GROUP BY `year`
ORDER BY `year`;

2.
SELECT COUNT(*) AS `numero_insegnanti`, `office_address` AS `ufficio`
FROM `teachers`
GROUP BY `office_address`;

3.
SELECT AVG(`vote`) AS `media`, `exam_id` AS `appello`
FROM `exam_student`
GROUP BY `appello`;

