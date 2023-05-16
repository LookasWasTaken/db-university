## JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
- SELECT `students`.`surname`, `students`.`name`, `students`.`registration_number`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
- SELECT `degrees`.`name`, `degrees`.`level`, `departments`.`name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale" AND `departments`.`name` = "Dipartimento di Neuroscienze";

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
- SELECT *
FROM `course_teacher`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`surname` = "Amato" AND `teachers`.`name` = "Fulvio" AND `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome
- SELECT `students`.`surname`, `students`.`name`, `degrees`.`name`, `departments`.`name` 
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
- SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`surname`, `teachers`.`name`
FROM `course_teacher`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
ORDER BY `degrees`.`name`, `courses`.`name`, `teachers`.`surname`, `teachers`.`name`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
- SELECT DISTINCT `teachers`.*
FROM `course_teacher`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per
superare ciascuno dei suoi esami, stampando anche il voto massimo e filtrare i tentativi con voto minimo 18.
SELECT `students`.`id`, `students`.`surname`, `students`.`name`, `courses`.`name`, `courses`.`id`
COUNT(`exam_student`.`vote`) AS `attempts_number`,
MAX(`exam_student`.`vote`) AS `highest_vote`,
FROM `students`
JOIN `exam_student` ON `students`.`id` = `exam_student`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exam`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`
HAVING `highest_vote` >= 18;
