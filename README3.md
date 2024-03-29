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

4.
SELECT COUNT(*) AS `number`, `department_id` AS `dipartimento`
FROM `degrees`
GROUP BY `dipartimento`;

<!-- join -->

1.
SELECT `students`.`name` AS `name_strudent`
FROM `degrees`
JOIN `students`
ON `degrees`.`id`= `students`.`degree_id`
WHERE `degrees`.`name`= 'Corso di Laurea in Economia';

2.
SELECT `degrees`.`name` AS `name_courses_of_magistral`
FROM `departments`
JOIN `degrees`
ON `departments`.`id`= `degrees`.`department_id`
WHERE `departments`.`name`= 'Dipartimento di Neuroscienze'
AND `degrees`.`name` LIKE 'Corso di Laurea Magistrale%';

3.
SELECT `courses`.`name` AS `name_corso_di_Fulvio`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id`= `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id`=`teachers`.`id`
WHERE `teachers`.`name`='Fulvio'
AND `teachers`.`surname`='Amato';

5.
SELECT `degrees`.`name` AS `nome_corso_laurea`, `courses`.`name` as `nome_corso`, `teachers`.`name` AS `teachers_name`, `teachers`.`surname` AS `teachers_surname`
FROM `degrees`
JOIN `courses`ON `degrees`.`id`= `courses`.`degree_id`
JOIN`course_teacher` ON `courses`.`id`= `course_teacher`.`course_id`
JOIN`teachers` ON `course_teacher`.`teacher_id`=`teachers`.`id`;

