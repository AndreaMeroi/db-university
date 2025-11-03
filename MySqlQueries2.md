# Group by
## Contare quanti iscritti ci sono stati ogni anno

SELECT YEAR(`enrolment_date`) AS `anno` , COUNT(id) AS `numero_iscritti`
FROM `students`
GROUP BY `enrolment_date`;

## Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT 	COUNT(`id`) AS `numero_insegnanti`, `office_address` AS `indirizzo_edificio`
FROM `teachers`
GROUP BY `office_address`;

## Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`vote`) AS `media_voto`, `exam_id` AS `appello_esame`
FROM `exam_student`
GROUP BY `exam_id`
ORDER BY `media_voto`DESC;

## Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(`id`) AS `numero_corsi_di_laurea`, `department_id`AS `dipartimento`
FROM `degrees`
GROUP BY `department_id`;

#JOINS
## Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.name, `degrees`.name
FROM `students`
JOIN `degrees`
ON `degrees`.id = `students`.`degree_id`
WHERE `degrees`.NAME = "Corso di Laurea in Economia";

## Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `departments`.name AS `dipartimento`, `degrees`.name AS `corsi_di_laurea`
FROM `degrees`
JOIN `departments`
ON `departments`.id = `degrees`.`department_id`
WHERE `departments`.name = "Dipartimento di Neuroscienze";

## Selezionare tutti i corsi in cui insegna Fulvio Amato id=44

SELECT `courses`.name AS `nome_corso`, `teachers`.name AS `nome_insegnante`, `teachers`.surname AS `cognome_insegnante`
FROM `course_teacher`
JOIN `courses`
ON `courses`.id = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.id = `course_teacher`.`teacher_id`
WHERE `teachers`.id = 44;

## Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.surname AS `cognome`, `students`.name AS `nome`, `degrees`.name AS `corso_di Laurea`, `departments`.name AS `dipartimento`
FROM `students`
JOIN `degrees`
ON `degrees`.id =`students`.`degree_id`
JOIN `departments`
ON `departments`.id = `degrees`.`department_id` 
ORDER BY `students`.surname ASC;

## Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti 

SELECT `degrees`.name AS `corso_di_laurea`, `courses`.name AS `corso`, `teachers`.surname AS `cognome`, `teachers`.name AS `nome`
FROM `course_teacher`
JOIN `teachers`
ON `teachers`.id = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.id = `course_teacher`.`course_id`
JOIN `degrees`
ON `degrees`.id = `courses`.`degree_id`
ORDER BY `degrees`.name ASC;

## Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.surname AS `cognome`, `teachers`.name AS `nome`, `departments`.name AS `dipartimento`
FROM `course_teacher`
JOIN `courses`
ON `courses`.id = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.id = `course_teacher`.`teacher_id`
JOIN `degrees`
ON `degrees`.id = `courses`.`degree_id`
JOIN `departments`
ON `departments`.id = `degrees`.`department_id`
WHERE `departments`.name = "Dipartimento di Matematica"
ORDER BY `teachers`.surname ASC;


## BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

SELECT `students`.id AS `id_studente`,ANY_VALUE(`exams`.id) AS id_esame,`courses`.id AS `id_corso`,ANY_VALUE(`students`.name) AS nome, ANY_VALUE(`students`.surname) AS cognome,COUNT(*) AS numero_tentativi,MAX(`exam_student`.vote) AS `voto_massimo`
FROM `exam_student`
JOIN `students`
ON `students`.id = `exam_student`.`student_id`
JOIN `exams`
ON `exams`.id = `exam_student`.`exam_id`
JOIN `courses`
ON `courses`.id = `exams`.`course_id`
GROUP BY `students`.id, `courses`.id
HAVING `voto_massimo`> 18 


 



