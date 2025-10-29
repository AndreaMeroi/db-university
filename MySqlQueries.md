SELECT *
FROM `students`
WHERE `date_of_birth` LIKE '1990%';

SELECT *
FROM `courses`
WHERE `cfu`> '10';

SELECT *
FROM `students`
WHERE `date_of_birth`< '1995-10-01';

SELECT *
FROM `courses`
WHERE `period` = 'I semestre'
AND `year`= '1';

SELECT *
FROM `exams`
WHERE `hour`> '14:00:00'
AND `date`= '2020-06-20';

SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';

SELECT `id`
FROM `departments`;

SELECT *
FROM `teachers`
WHERE `phone` IS NULL;







