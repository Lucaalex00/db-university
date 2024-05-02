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
