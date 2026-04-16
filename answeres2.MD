USE db_university;

-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT students.name, students.surname
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia';

-- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT degrees.name
FROM degrees
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Neuroscienze'
AND degrees.level = 'magistrale';

-- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT courses.name
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
WHERE course_teacher.teacher_id = 44;

-- 4. Selezionare tutti gli studenti con i dati del corso di laurea e del dipartimento, in ordine alfabetico
SELECT students.surname, students.name, degrees.name AS corso, departments.name AS dipartimento
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.name;

-- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT degrees.name, courses.name, teachers.surname, teachers.name
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id;

-- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica
SELECT DISTINCT teachers.surname, teachers.name
FROM teachers
JOIN course_teacher ON teachers.id = course_teacher.teacher_id
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Matematica';




-- 1. Contare quanti iscritti ci sono stati ogni anno
SELECT YEAR(enrolment_date) AS anno, COUNT(*) AS iscritti
FROM students
GROUP BY YEAR(enrolment_date);

-- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT office_address, COUNT(*) AS n_docenti
FROM teachers
GROUP BY office_address;

-- 3. Calcolare la media dei voti di ogni appello d'esame
SELECT exam_id, AVG(vote) AS media
FROM exam_student
GROUP BY exam_id;

-- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT department_id, COUNT(*) AS n_corsi
FROM degrees
GROUP BY department_id;
