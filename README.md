
# SQL Training 

Given tables
* users
    * type - teacher / student
* courses
* enrollments

Create a SQL query for the ff

1. How many students are there
```sql
select COUNT(*) from users WHERE type='student';
```
2. How many teachers are there
```sql
select COUNT(*) from users WHERE type='teacher';
```
3. Who is the teacher that teaches the most courses
```sql
with teacher_courses as (
    select count(c.name) courses, u.first_name, u.last_name from users u 
left join courses c on c.teacher_id=u.id
where u.type='teacher'
GROUP BY u.first_name, u.last_name
)
select * from teacher_courses order by courses desc;
```
4. How many students are there in each course
```sql
select count(e.student_id) Students, c.name, c.id from courses c 
left join enrollments e on c.id=e.course_id
GROUP BY c.name, c.id;
```
5. How many unique students does a teacher have
6. What are the courses that student kpeartree0@mac.com is enrolled in
7. Who are the teachers that teach student bdoucea@marketwatch.com show their email and course handled
8. What are the courses that teacher fjochen14@dedecms.com handles
9. What courses does each teacher teach? express in a json array type column
10. Show all the students taught by fjochen14@dedecms.com and show the course they are studying. ( students can have more than 1 course )
11. Create a new student and enroll it to 3 subjects
12. Create a new course assign 10 students
13. Change the course name Math to Mathematics
14. Change the teacher of Science to someone else
15. Create a function that let’s you enroll a student to a subject using their email and the course name
16. Create a trigger that won’t allow you to create a course with a user_id that is not type ‘teacher’
