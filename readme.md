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
