1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni (3392)
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
13. Selezionare il voto medio di superamento d'esame per ogni corso, con anche i dati del corso di laurea associato, ordinati per media di voto decrescente


# QUERIES
0. C:\MAMP\bin\mysql\bin\mysql -u root -p

1. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `students`;
- SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;

2. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `courses`;
- SELECT * FROM `courses` WHERE `cfu` > 10;

3. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `students`;
- SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30 ORDER BY `date_of_birth`;

4. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `courses`;
- SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = 1;

5. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `exams`;
- SELECT * FROM `exams` WHERE `date` = "2020-06-20" AND `hour` >= "14:00:00";

6. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `degrees`;
- SELECT * FROM `degrees` WHERE `level` = "magistrale";

7. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `departments`;
- SELECT COUNT(*) as "Departments" FROM `departments`;

8. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `teachers`;
- SELECT COUNT(*) FROM `teachers` WHERE `phone` is NULL;

9. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `courses`;
- SELECT COUNT(*) AS `total_courses`, `cfu` FROM `courses` GROUP BY `cfu`;

10. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `students`;
- SELECT COUNT(*) AS `total_students`, YEAR(`date_of_birth`) AS `year_of_birth` FROM `students` GROUP BY `year_of_birth`;

11. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `exam_student`;
- SELECT MIN(`vote`) AS `lowest_vote`, `exam_id` FROM `exam_student` GROUP BY `exam_id`;

12. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `exams`;
- SELECT COUNT(*) AS `total_exams`, DAY(`date`) AS `day_of_exam` FROM `exams` WHERE MONTH(`month_of_exam`) = 7 GROUP BY `day_of_exam`;


12. SHOW databases;
- USE `91_university`;
- SHOW tables;
- DESCRIBE `degrees`;
- SELECT `courses`.`id`, `courses`.`name`, `degrees`.`name` FROM `72_university`.`courses` JOIN `72_university`.`degrees` ON `courses`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = "Corso di Laurea in Informatica";

13. SHOW databases;
- USE `91_university`;
- SHOW tables;
- SELECT AVG(`exam_student`.`vote`) AS `average_vote`, `courses`.`name`, `degree`.`name`
FROM `exam_student`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
GROUP BY `courses`.`id`
ORDER BY `average_vote` DESC;