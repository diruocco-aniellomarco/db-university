**Query 1**

- **Selezionare tutti gli studenti nati nel 1990**

SELECT \* FROM `students` WHERE `date_of_birth` LIKE '1990%';

**Query 2**

- **Selezionare tutti i corsi che valgono più di 10 crediti**

SELECT \* FROM `courses` WHERE `cfu` > 10;

**Query 3**

- **Selezionare tutti i corsi che valgono più di 10 crediti**

SELECT \* FROM `students` WHERE `date_of_birth` < '1993%';

**Query 4**

- **Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea**

SELECT \* FROM `courses` WHERE `period` LIKE 'I semestre' AND `year` LIKE 1;

**Query 5**

- **Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020**

SELECT \* FROM `exams` WHERE `date` LIKE '2020-06-20' AND `hour` > '14:00';

**Query 6**

- **Selezionare tutti i corsi di laurea magistrale**

SELECT \* FROM `degrees` WHERE `level` LIKE 'magistrale';

**Query 7**

- **Da quanti dipartimenti è composta l'università?**

SELECT COUNT(\*) AS `number_deparments` FROM `departments`;

**Query 8**

- **Quanti sono gli insegnanti che non hanno un numero di telefono?**

SELECT COUNT(\*) FROM `teachers` WHERE `phone` IS NULL;

---

09/10/2023

**- - GROUP BY - -**

**Query 1**

- **Contare quanti iscritti ci sono stati ogni anno**

SELECT COUNT(\*) AS `number_members`, YEAR(`enrolment_date`) AS `enrolment_year` FROM `students` GROUP BY YEAR(`enrolment_date`);

**Query 2**

- **Contare gli insegnanti che hanno l'ufficio nello stesso edificio**

SELECT COUNT(\*), `office_address` FROM `teachers` GROUP BY `office_address`;

**Query 3**

- **Calcolare la media dei voti di ogni appello d'esame**

SELECT `exam_id`, AVG(`vote`) AS `avg_vote` FROM `exam_student` GROUP BY `exam_id`;

**Query 4**

- **Contare quanti corsi di laurea ci sono per ogni dipartimento**

SELECT `department_id`, COUNT(`name`) AS `number_degrees` FROM `degrees` GROUP BY `department_id`;

---

**- - JOIN - -**

**Query 1**

- **Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia**

SELECT `students`.`name`, `students`.`surname`,`degrees`.`name` AS `degrees_name` FROM `students` INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

**Query 2**

- **Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze**

SELECT `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS `department_name` FROM `degrees` INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` WHERE `degrees`.`level`= 'magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';

**Query 3**

- **Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)**

SELECT `courses`.`id` AS `courses_id` ,`courses`.`name` AS `courses_name` ,`teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname` FROM `courses` INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` WHERE `teachers`.`name` = 'Fulvio' AND `teachers`.`surname` = 'Amato';

**Query 4**

- **Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome**

SELECT `students`.`name` AS `students_name`, `students`.`surname` AS `students_surname`, `degrees`.`name` AS `degrees_name`, `departments`.`name` AS `departments_name` FROM `students` INNER JOIN `degrees` ON `degrees`.id = `students`.`degree_id` INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` ORDER BY `students_surname`, `students_name` ASC;

**Query 5**

- **Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti**

SELECT `degrees`.`name` `degree_name`, `courses`.`name` `course_name`, `teachers`.`name` `teacher_name`, `teachers`.`surname` `teacher_surname` FROM `degrees` INNER JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` ORDER BY `degree_name` ASC;

**Query 6**

- **Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica**

SELECT DISTINCT `teachers`.`id`, `teachers`.`name` `teacher_name`, `teachers`.`surname` `teacher_surname`, `departments`.`name` `department_name` FROM `teachers` INNER JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id` INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` INNER JOIN `degrees` ON `degrees`.`id` =`courses`.`degree_id` INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` WHERE `departments`.`name` = 'Dipartimento di Matematica' ORDER BY `teachers`.`id` ASC;
