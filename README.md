# db-university


1. Selezionare tutti gli studenti nati nel 1990 (160);

query: SELECT * FROM `students` WHERE YEAR (`date_of_birth`)= "1990";
risultato:(160) conforme.


2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

query: SELECT * FROM `courses` WHERE`cfu`>"10";
risultato:(479)conforme


3. Selezionare tutti gli studenti che hanno più di 30 anni

query: SELECT* from `students`
 WHERE TIMESTAMPDIFF(year,`date_of_birth`,CURDATE())>30;
risultato:ok


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286).

query: SELECT * 
FROM `courses` WHERE `period`="I semestre" AND`year`=1
risultato:ok

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21).

query:
 SELECT * FROM `exams` WHERE `date`='2020-06-20' AND HOUR(`hour`) > "14" ORDER BY `exams`. `hour`ASC
risultato:non coretta


6. Selezionare tutti i corsi di laurea magistrale (38)

query:
SELECT * FROM `degrees` WHERE `levelSELECT`="magistrale"
risultato:(38)

7. Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(*) 
FROM`departments` 
risultato:(12)


8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50

query: 
SELECT COUNT(*) AS "numero di telefono" FROM `teachers`
 WHERE `phone`is null
risultato:


1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

query: 
 SELECT `students`.`name`,`students`.`surname`,`students`.`registration_number` FROM `students` JOIN `degrees`ON`students`.`degree_id`=`degrees`.`id` 
 WHERE `degrees`.`name`="Corso di laurea in Economia"
risultato:(68)


2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze

query: 
SELECT `departments`.`name`,`degrees`.`name`,`degrees`.`level` 
 FROM `departments` 
 JOIN`degrees`
 ON `departments`.`id`=`degrees`.`department_id` 
 WHERE `departments`.`name`="Dipartimento di Neuroscienze"
risultato:(7)

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

query: SELECT `teachers`.`id`AS"ID_insegnante",`courses`.`name`, `courses`.`description` 
FROM `courses` JOIN`course_teacher`ON`course_teacher`.`course_id`=`courses`.`id` JOIN`teachers`ON`course_teacher`.`teacher_id`=`teachers`.`id` 
WHERE `teachers`.`name`="Fulvio" AND`teachers`.`surname`="Amato"
risultato:(11)

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome


query:SELECT`students`.`name`AS"nome_studente" ,`students`.`surname`AS"_Cognome_studente",`students`.`registration_number`,`degrees`.`id`AS"nome_laurea",`departments`.`name`AS"nome_dipartimento" 
FROM`students` 
join `degrees`on `students`.`degree_id`=`degrees`.`id` join`departments` ON `departments`.`id`=`degrees`.`department_id` ORDER BY `students`.`surname`,`students`.`name`




5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti


query:
SELECT`degrees`.`name`AS"nome_laurea",`courses`.`name`AS "nome_corso",`teachers`.`name`AS"nome_insegnante",`teachers`.`surname`AS"cognome_insegnante" FROM`degrees` 
join`courses`ON `degrees`.`id`=`courses`.`degree_id` 
join`course_teacher`on `courses`.`id`=`course_teacher`.`course_id` join`teachers`ON`teachers`.`id`=`course_teacher`.`teacher_id` 
risultato:(1317)



6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

query: SELECT DISTINCT `teachers`.`name` AS "nome_insegnante",`teachers` . `surname`AS "cognome_insegnante" from`degrees` join `courses` ON `degrees`.`id`=`courses`.`degree_id` join `course_teacher` ON `courses`.`id`=`course_teacher`.`course_id` join`teachers`ON `teachers`.`id`=`course_teacher`.`teacher_id` join`departments`ON`departments`.`id`+`degrees`.`department_id` WHERE`departments`.`name`="Dipartimento di Matematica" ORDER BY `cognome_insegnante`ASC
risultato:

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per
superare ciascuno dei suoi esami


query: 
risultato: