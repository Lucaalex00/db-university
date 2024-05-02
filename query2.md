## Group by
1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
## Joins
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

## BONUS: 
1. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

//////////////////////////////////////////////////////////////////////////////

**GROUP BY**

1. 
SELECT YEAR(`enrolment_date`) AS anno_iscrizione, COUNT(*) AS numero_iscritti
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY anno_iscrizione;

2. 
SELECT `office_address`, COUNT(*) AS numero_insegnanti
FROM `teachers`
GROUP BY `office_address`;
<!-- SE DOVESSI FARE UNA CONDIZIONE DEL TIPO "dammi il valore solo se è > 1" Devo usare HAVING piuttosto che WHERE perchè dopo il group by non posso utilizzare quest'ultimo. -->

3. 
SELECT AVG(`vote`) as media_voti
FROM `exam_student`;
<!-- 17.9573 -->
<!-- Utilizzando AVG fai la media fra x valori (in questo caso i voti) -->

4. 
SELECT departments.name AS dipartimento, COUNT(degrees.id) AS numero_corsi_laurea
FROM `departments`
JOIN `degrees` ON departments.id = degrees.department_id
GROUP BY departments.name;

**JOINS**

1. 
SELECT `students`.*
FROM `students`
JOIN `degrees` ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia';

2. 
SELECT `degrees`.*
FROM degrees
JOIN `departments`
ON degrees.department_id = departments.id
WHERE degrees.level = "Magistrale"
AND departments.name ="Dipartimento di Neuroscienze";
<!-- 
44 | ID
7 | Department_ID
Corso di Laurea Magistrale in Odontoiatria e Prote... | NAME
magistrale | LEVEL
Via Mariani 185 | ADDRESS
odontoiatria-e-protesi-dentaria@uni.it | EMAIL
www.odontoiatria-e-protesi-dentaria.uni.it  | WEBSITE
-->

3. 
SELECT `courses`.*
FROM `courses`
JOIN `course_teacher` ON courses.id = course_teacher.course_id
JOIN `teachers` ON course_teacher.teacher_id = teachers.id
WHERE teachers.id= 44;
<!-- 11 -->

4. 
SELECT `students`.name as nome_studente, `students`.surname as cognome_studente, `degrees`.*, departments.name AS nome_dipartimento
FROM `students`
JOIN `degrees` ON students.degree_id = degrees.id
JOIN `departments` ON degrees.department_id = departments.id  
ORDER BY students.surname ASC, students.name ASC;
<!-- 5000 -->

5. 
SELECT `degrees`.name as nome_laurea, `courses`.name as nome_corso, `teachers`.*
FROM `degrees`
JOIN `courses` ON courses.degree_id = degrees.id
JOIN `teachers` ON teachers.id = degrees.id;
**OPPURE**
SELECT `degrees`.name as nome_laurea, `courses`.name as nome_corso, `teachers`.*
FROM `degrees`
JOIN `courses` ON `courses`.degree_id = degrees.id
JOIN `course_teacher` ON course_teacher.course_id = courses.id
JOIN `teachers` ON teachers.id = course_teacher.teacher_id;

<!-- IN BASE A SE SI VUOLE COLLEGARE ANCHE ALLA TABELLA DEGLI INSEGNATI CHE FANNO IL CORSO O SOLO ALL'INSEGNANTE -->
<!-- 1317 -->

6. 
SELECT DISTINCT `teachers`.*, `departments`.name as nome_dipartimento
FROM `teachers`
JOIN `course_teacher` ON teachers.id = course_teacher.teacher_id
JOIN `courses` ON course_teacher.course_id = courses.id
JOIN `degrees` ON courses.degree_id = degrees.id
JOIN `departments` ON degrees.department_id = departments.id
WHERE `departments`.name = 'Dipartimento di Matematica'
ORDER BY teachers.id ASC;
<!-- Il DISTINCT dopo il SELECT fa un controllo su i valori che si ripetono non mostrandone più di uno per tipo -->
<!-- 54 -->