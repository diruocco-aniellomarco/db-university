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
