# SQL---study-material

SQL Task 1
--1. Display first name and last name as full name, salary, commission pct, and hire date for employees with salary less than 10000.

SELECT
 first_name || ' ' || last_name as "full name", salary, commission_pct, hire_date 
FROM
 hr.employees 
WHERE
 salary< 10000;

--2. Display city names (without repeated names) in ascending order from locations table.

SELECT
 distinct city   
FROM
 hr.locations 
ORDER BY
 city asc;

--3. Display the first name, hire date and job ID of the employees who is either IT Programmer or Sales Manager, and hired between 2002 and 2005.

SELECT
 first_name, hire_date, job_id 
FROM
 hr.employees 
WHERE
 (job_id='IT_PROG' or job_id='SA_MAN') AND hire_date between '01-JAN-2002' and '31-DEC-2005';


--4. Display details from jobs table in the descending order of the job title.

SELECT
 * 
FROM
 hr.jobs 
ORDER BY
 job_title desc;

--5. Display details of the employees where commission percentage is null and salary in the range 5000 to 10000 and department id is 30.

SELECT
 first_name || ' ' || last_name as "full name", commission_pct, salary, department_id 
FROM
 hr.employees 
WHERE
 (commission_pct is Null) AND ( salary BETWEEN 5000 AND 10000) AND department_id=30;


--6. Display employees who joined after 1st January 2008.

select first_name || ' ' || last_name as "full name", hire_date from hr.employees where hire_date> '01-JAN-2008'

--7. Display details of employees with ID 150, 160 or 170.

select first_name || ' ' || last_name as "full name", employee_id from hr.employees where employee_id in(150,160,170)

--8. Display employees where the first name or last name starts with S.

select first_name || ' ' || last_name as "full name" from hr.employees where first_name like 'S%' or last_name like 'S%'
--9. Display the length of first name for employees where last name contain character ‘b’ after 3rd position.

select LENGTH(first_name), last_name from hr.employees where last_name like '___%b%'

Task 2

1.Write a query in SQL to display job Title, the difference between minimum and maximum salaries for those jobs which max salary within the range 12000 to 18000.

select job_title, max_salary-min_salary  as difference from hr.jobs where max_salary between 12000 and 18000

2. Display the details of the employees who have no commission percentage and whose salary is within the range 7000 to 12000 for those employees who are not working in the departments
50,30 and 80.

select * from  hr.employees where commission_pct is null and (salary between 7000 and 12000) and not (department_id in (50,30,80))


3) Write a query in SQL to display the full name (first name and last name), hire date, commission percentage, email and telephone separated by '-', and salary for those employees whose salary is above 11000 and make the result set in a descending order by the full name.

select * from (select first_name || ' ' || last_name as full_name, hire_date, commission_pct, email || ' _ ' || phone_number, salary  from hr.employees where salary> 11000) order by full_name


4) Write a query in SQL to display the first and last name, and salary for those employees whose first name is ending with the letter “m” and they have been hired before June 5th, 2010.

select first_name, last_name, salary, hire_date from hr.employees where first_name like '%m' and hire_date < '05-JUN-2010'

5) Display the full name (first and last), the phone number and email separated by hyphen, and
salary, for those employees whose salary is not within the range of 9000 and 17000 and
commission is not null. The column headings assign with Full_Name, Contact _Details and
Remuneration respectively.

select first_name || ' ' || last_name as full_name, phone_number|| '-' || email as contact_details, salary as Remuneration from hr.employees where (salary not between 9000 and 17000) and commission_pct is not null





6) Write a query in SQL to display all the information about the department Marketing.

select * from hr.departments where department_name= 'Marketing'



7) Write a query to display data from job_history and make the result set in descending order by the employee_id and ascending order by start date.

select * from hr.job_history order by employee_id desc, start_date asc


8) Write a query to display job_id and salary of employees whose phone number starts with 515 or 590 and was hired after 2003 by sorting hire_date and salary in ascending way.

SELECT job_id, salary
FROM hr.employees
WHERE phone_number LIKE '515%' OR phone_number LIKE '590%'
AND hire_date > '01-JAN-03'
ORDER BY hire_date ASC, salary ASC;

9) Write a query to display employees who were hired in 2001.

select * from hr.employees where hire_date between  '01-JAN-01' and  '31-DEC-01'



10) Write a query to display employees’ first and last name who were not hired in 2006 and 2007.

select first_name,last_name, hire_date from hr.employees where hire_date not between '01-JAN-06' and '31-DEC-07'





11) Write a query to display email, job_id and first name of employees whose hired year was 2007 or hired month was 1.

SELECT email, job_id, first_name
FROM hr.employees
WHERE EXTRACT(YEAR FROM hire_date) = 2007 OR EXTRACT(MONTH FROM hire_date) = 1;


12) Write a query to display details of employees who was hired after 2007 or salary is less than
10000.

select * from hr.employees where extract(year from hire_date)>2007 or salary<10000

Task 3
1. Display employees who joined in the month of May.
    select first_name || ' ' || last_name as full_name, hire_date from hr.employees where extract(month from hire_date) = '05'

2. Display employees who joined in the current year.
    select first_name || ' ' || last_name as full_name, hire_date from hr.employees where extract(year from hire_date) = 2022

3. Display the number of days between system date and 1st January 2011.
    select months_between(sysdate,'01-JAN-11')*30 FROM HR.EMPLOYEES

4. Display maximum salary of employees.
    select max (salary) from hr.employees

5. Display number of employees in each department.
    select count(*), department_id from hr.employees group by department_id

6. Display number of employees who joined after 15th of month.
      select count(*) from hr.employees where extract (day from hire_date) >15

7. Display average salary of employees in each department who have commission percentage.
select avg(salary), department_id from hr.employees where commission_pct is not null group by department_id

    
8. Display job ID for jobs with average salary more than 10000.
    select job_id, avg(salary) from hr.employees having avg(salary)>10000 group by job_id

      

9. Display job ID, number of employees, sum of salary, and difference between the highest
salary and the lowest salary of the employees for all jobs.
    select job_id, count(*), sum(salary), max(salary)-min(salary) as difference from hr.employees group by job_id

10.Display manager ID and number of employees managed by the manager.
    select manager_id, count(*) from hr.employees where manager_id is not null group by manager_id ;

task4

--1. Show minimum, average and maximum salary in last 15 years according to job id.

SELECT 
  job_id, 
  MIN(salary) AS minimum_salary, 
  AVG(salary) AS average_salary, 
  MAX(salary) AS maximum_salary
FROM 
  hr.employees
WHERE 
  EXTRACT(YEAR FROM sysdate) - EXTRACT(YEAR FROM hire_date) <= 15
GROUP BY 
  job_id;

--2. How many employees hired after 2005 for each department?

SELECT
 count(*), job_id 
FROM hr.employees
 Where
 EXTRACT(year from hire_date)>2005 
GROUP BY
 job_id;

--3. Write a query to show departments in which the difference between maximum and minimum salary is greater than 5000.

SELECT
 department_id, max(salary), min(salary) 
FROM
 hr.employees 
HAVING
 max(salary)-min(salary) > 5000  
Group by
department_id;
--4. Display salaries of employees who has not commission pact according to departments (without using where).

SELECT
    sum(CASE WHEN commission_pct IS NULL THEN salary ELSE 0 END), department_id 
    FROM hr.employees 
    GROUP BY
    department_id;

--5. How many people has job id with average salary between 3000 and 7000?

SELECT COUNT(*) 
FROM hr.employees 
WHERE job_id IN (
  SELECT job_id 
  FROM hr.employees 
  GROUP BY job_id 
  HAVING AVG(salary) BETWEEN 3000 AND 7000
);

--6. Find number of employees with same name.

SELECT
    first_name, count(*)
    FROM hr.employees 
    HAVING count(*)>1
    GROUP BY 
first_name;

--7. How many people with the same phone code work in departments 50 and 90?
SELECT
    substr(phone_number,1,3) as phone_code, COUNT(*)
    FROM
    hr.employees
    WHERE 
    department_id in (50,90)
    GROUP BY
    substr(phone_number,1,3);

--8. Display departments with average number of employees more than 5 in spring and autumn.

SELECT
    department_id, count(employee_id)
    FROM
    hr.employees
    WHERE
    (EXTRACT(MONTH FROM hire_date) between 3 and 5) OR
    (EXTRACT(month FROM hire_date) between 9 and 11)
    HAVING COUNT(employee_id) >5
    GROUP BY
    department_id;

--9. How many employees work in departments which has maximum salary more than 5000?
SELECT
    department_id, count(employee_id)
    FROM hr.employees
    HAVING 
    MAX(salary)>5000
GROUP BY
    department_id

--10.Change second letter of employees’ names with the last letter and display.
SELECT
    first_name, substr(first_name,1,1) || substr(first_name, length(first_name),1) || substr(first_name,3,length(first_name)-3)||substr(first_name,2,1)
    FROM
    hr.employees;


TASK 5

--1. Display last name, job title of employees who have commission percentage and belongs to department 30.
SELECT
    first_name, job_title
    FROM
    hr.employees a  left join hr.jobs b  on a.job_id= b.job_id
    WHERE
    commission_pct is not null and department_id=30;

--2. Display department name, manager name, and salary of the manager for all managers whose experience is more than 5 years.

SELECT
    m.first_name, m.salary, e.first_name, d.department_name, m.manager_id
FROM
    hr.employees e
LEFT JOIN
    hr.employees m
ON
    m.employee_id=e.manager_id
LEFT JOIN
    hr.departments d
ON
    d.department_id=e.department_id
WHERE
    extract(year from current_date)-extract(year from e.HIRE_DATE)>5;


--3. Display employee name if the employee joined before his manager.


SELECT  
e.first_name, e.employee_id, m.hire_date as mngr_hire_date, e.manager_id, e.hire_date as emp_hiree_date
FROM 
hr.Employees e
INNER JOIN 
hr.Employees m
ON 
e.manager_id = m.employee_id
WHERE
 e.hire_date < m.hire_date;

--4. Display employee name, job title for the jobs, employee did in the past where the job was done less than six months.

SELECT
 e.first_name, j.job_title,jb.start_date, jb.end_date 
    FROM
 hr.employees e left join hr.jobs j on e.job_id=j.job_id left join hr.job_history jb on j.job_id=jb.job_id 
    WHERE
 (end_date-start_date)<30*6;

--5. Display department name, average salary and number of employees with commission within the department.
SELECT
    avg(salary), department_name, count(*) 
    FROM
    hr.departments d left join hr.employees e on d.department_id=e.department_id 
    WHERE
    commission_pct is not null 
    GROUP BY
    department_name;

--6. Display employee name and country in which he is working.

SELECT
    a.first_name, d.country_name  
    FROM
    hr.employees a left join hr.departments b on a.department_id=b.department_id 
left join hr.locations c on b.location_id=c.location_id 
left join hr.countries d on c.country_id=d.country_id;


TASK 6

---1 Display the first promotion year for each employee.
SELECT
    employee_id, extract(year from min(end_date)) as promotion_year
from hr.job_history
group by employee_id
having count(EMPLOYEE_ID)>1;

---2 Display location, city and department name of employees who have been promoted more than once.


select e.employee_id,e.first_name, l.city, d.department_name ,extract(year from min(jh.end_date)) promotion_year
from hr.locations l
left join hr.departments d
on l.location_id=d.location_id
left join hr.employees e
on d.department_id=e.department_id
left join hr.job_history jh
on jh.job_id = e.job_id
group by e.employee_id, l.city, d.department_name, e.first_name
having count(e.employee_id) > 2;

---3 Display minimum and maximum “hire_date” of employees work in IT and HR departments.
select d.department_name, min(e.hire_date), max(e.hire_date)
from hr.employees e
left join hr.departments d
on e.department_id=d.department_id
where d.department_name='IT' or department_name='Human Resources'
group by d.department_name;

---4 Find difference between current date and hire dates of employees after sorting them by hire date, then show difference in days, months and years.

SELECT
 Current_Date, hire_date Hire_Date, round(sysdate-hire_date,0) Day_Difference,
round(months_between(sysdate,hire_date),0) Month_Difference,
EXTRACT(year from sysdate)-EXTRACT(year from hire_date) Year_Difference
FROM
 hr.employees
ORDER BY 
hire_date;

---5 Find which departments used to hire earliest/latest.

SELECT
    e.hire_date, e.department_id, d.department_name
FROM
    hr.employees e
LEFT JOIN
    hr.departments d
ON
    e.department_id=d.department_id
WHERE
    e.hire_date=(select min(hire_date) from hr.employees)
union
SELECT
    e.hire_date, e.department_id, d.department_name
FROM
    hr.employees e
LEFT JOIN
    hr.departments d
ON
    e.department_id=d.department_id
WHERE
    e.hire_date=(select max(hire_date) from hr.employees);

--6. Create a category called “seasons” and find in which season most employees were hired.

 
 SELECT
     * 
     FROM
     (select case
when extract(month from hire_date) in ('12','01','02') then 'Winter'
when extract(month from hire_date) in ('03','04','05') then 'Spring'
when extract(month from hire_date) in ('06','07','08') then 'Summer'
else 'Autumn'
end Season,
count(employee_id) Number_employees_id
FROM
     hr.employees
GROUP BY
     case
when extract(month from hire_date) in ('12','01','02') then 'Winter'
when extract(month from hire_date) in ('03','04','05') then 'Spring'
when extract(month from hire_date) in ('06','07','08') then 'Summer'
else 'Autumn'
end)
ORDER BY
     Number_employees_id desc
fetch first 1 row only;


---7. Find the cities of employees with average salary more than 5000.

SELECT
    avg(salary), city 
    FROM
    hr.employees e 
LEFT JOIN
    hr.departments d 
    ON
    e.department_id=d.department_id 
LEFT JOIN
    hr.locations l 
    ON
    d.location_id=l.location_id 
    WHERE
    city is not null
 HAVING
    avg(salary)>5000 
    GROUP BY
    city;

Task 7

---1 According to the given diagram create STUDENTS , ACTIVITIES and SCHEDULE tables. (PK – PRIMARY KEY,FK – FOREIGN KEY, * - NOT NULL )

 

create table STUDENTS (
S_ID int not null,
FIRST_NAME varchar2(25) not null,
LAST_NAME varchar2(25),
EMAIL varchar2(20),
PHONE_NUMBER varchar2(20) not null,
primary key (S_ID)
);

desc STUDENTS;

create table activities (
A_ID number(3) not null,
A_NAME varchar(20),
COST number,
    primary key (A_ID));

desc activities;

create table SCHEDULE (
S_ID int,
A_ID number(3), 
S_DATE date,
constraint stu_act_sche_fk
foreign key (S_ID)
references STUDENTS (S_ID),
    foreign key (A_ID)
    REFERENCES activities (A_ID));

desc SCHEDULE;

---2 Insert data into students table from employees table.

INSERT INTO
 STUDENTS (S_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER)
SELECT
 EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER
FROM
 hr.employees;

select * from STUDENTS;

---3 Change phone number to ‘***’ for students with s_id > 200.
UPDATE
 STUDENTS 
SET
 PHONE_NUMBER = '***' where S_ID > 200;

select * from STUDENTS;

---4 Update first name and last names of students in Upper cases.
UPDATE
    STUDENTS 
    SET
    first_name=UPPER(first_name), last_name=UPPER(last_name);

select * from STUDENTS;


---5 Based on the students table populated with the following data, update the email to 'DSA' for all records whose s_id is greater than 150.
UPDATE
    STUDENTS 
    SET email = 'DSA' where S_ID > 150;

select * from STUDENTS;

---6 Create PROGRAMMERS table using records from EMPLOYEES where job_id contains ‘PROG’ substring
CREATE TABLE
    Programmers AS (SELECT EMPLOYEE_ID, first_name, last_name, EMAIL, PHONE_NUMBER, HIRE_DATE, JOB_ID
FROM
    hr.employees where job_id='IT_PROG'
);
SELECT * FROM programmers

--8.  Insert some date into SCHEDULE, then truncate and see results.

insert into SCHEDULE (S_DATE) values ('25-Apr-2022');
insert into SCHEDULE (S_DATE) values ('16-Nov-2021');
insert into SCHEDULE (S_DATE) values ('22-Feb-2022');
insert into SCHEDULE (S_DATE) values ('25-Dec-2021');
insert into SCHEDULE (S_DATE) values ('07-Jul-2022');
insert into SCHEDULE (S_DATE) values ('04-Jun-2022');
insert into SCHEDULE (S_DATE) values ('21-Oct-2021');
insert into SCHEDULE (S_DATE) values ('24-Aug-2021');
insert into SCHEDULE (S_DATE) values ('25-Jan-2022');
insert into SCHEDULE (S_DATE) values ('03-Sep-2021');
insert into SCHEDULE (S_DATE) values ('21-Jun-2022');
insert into SCHEDULE (S_DATE) values ('17-Nov-2021');
insert into SCHEDULE (S_DATE) values ('10-Dec-2021');
insert into SCHEDULE (S_DATE) values ('15-Jan-2022');
insert into SCHEDULE (S_DATE) values ('01-Apr-2022');
insert into SCHEDULE (S_DATE) values ('31-Jul-2022');
insert into SCHEDULE (S_DATE) values ('07-Oct-2021');
insert into SCHEDULE (S_DATE) values ('03-Aug-2022');
insert into SCHEDULE (S_DATE) values ('20-Jul-2022');
insert into SCHEDULE (S_DATE) values ('06-Apr-2022');
insert into SCHEDULE (S_DATE) values ('30-Aug-2021');
insert into SCHEDULE (S_DATE) values ('14-May-2022');
insert into SCHEDULE (S_DATE) values ('08-Apr-2022');
insert into SCHEDULE (S_DATE) values ('28-Dec-2021');
insert into SCHEDULE (S_DATE) values ('22-Apr-2022');
insert into SCHEDULE (S_DATE) values ('30-Jan-2022');
insert into SCHEDULE (S_DATE) values ('13-Mar-2022');
insert into SCHEDULE (S_DATE) values ('08-Jan-2022');
insert into SCHEDULE (S_DATE) values ('04-Jul-2022');
insert into SCHEDULE (S_DATE) values ('25-Oct-2021');
insert into SCHEDULE (S_DATE) values ('12-Jun-2022');
insert into SCHEDULE (S_DATE) values ('03-Jun-2022');
insert into SCHEDULE (S_DATE) values ('21-Feb-2022');
insert into SCHEDULE (S_DATE) values ('09-Jun-2022');
insert into SCHEDULE (S_DATE) values ('07-Oct-2021');
insert into SCHEDULE (S_DATE) values ('04-Apr-2022');
insert into SCHEDULE (S_DATE) values ('06-Mar-2022');
insert into SCHEDULE (S_DATE) values ('16-Nov-2021');
insert into SCHEDULE (S_DATE) values ('15-Mar-2022');
insert into SCHEDULE (S_DATE) values ('02-Nov-2021');
insert into SCHEDULE (S_DATE) values ('20-Jun-2022');
insert into SCHEDULE (S_DATE) values ('04-Nov-2021');
insert into SCHEDULE (S_DATE) values ('27-Apr-2022');
insert into SCHEDULE (S_DATE) values ('16-Aug-2021');
insert into SCHEDULE (S_DATE) values ('03-Jul-2022');
insert into SCHEDULE (S_DATE) values ('07-Oct-2021');
insert into SCHEDULE (S_DATE) values ('28-Dec-2021');

select * from schedule;
Truncate table schedule;

--9) Drop schedule table
DROP TABLE schedule;

--10. For any date given, write a script to find:

--a) The first and the last days of the next year;
SELECT trunc(sysdate)  from dual;

SELECT
 add_months(trunc(sysdate, 'YEAR'), 12) as first_day_of_next_year,
add_months(trunc(sysdate, 'YEAR'), 24)-1 as last_day_of_next_year
FROM
 Dual;

b) The first and the last days of the next month;

SELECT
 add_months(trunc(sysdate, 'MONTH'),1) as first_day_of_next_month,
add_months(trunc(sysdate, 'MONTH'),2)-1 as last_day_of_next_month
FROM
 Dual;

c) The first and the last days of the previous month.

SELECT
    add_months(trunc(sysdate, 'MONTH'), -1) as first_day_of_previous_month,
trunc(sysdate, 'MONTH')-1 as last_day_of_previous_month
FROM
    dual;

--- 11.Create a table named “Participants” which consists of first_name, last_name and salary (have to more than 10000).


CREATE TABLE
    Participants (first_name varchar2(100), last_name varchar2(100), salary number, CHECK (salary>10000));

Task 8

--1 Return the name of the employee with the lowest salary in department 90.

First solution)
 SELECT *
FROM
    hr.employees e
WHERE
    Salary = (select min(SALARY) from hr.employees where department_id = 90);

Second solution) 
SELECT
    department_id, first_name, salary, 
DENSE_RANK()
OVER(partition by department_id order by salary asc) drank,
RANK()
OVER(partition by department_id order by salary asc) prank
FROM hr.employees
WHERE
    salary=(select min(Salary) from hr.employees where department_id=90);

---2 Select the department name, employee name, and salary of all employees who work in the human resources or purchasing departments. 
--Compute a rank for each unique salary in both departments.

select * from hr.employees;
select * from hr.departments;

SELECT
 e.department_id, d.department_name, e.first_name, e.salary,
DENSE_RANK()
OVER (PARTITION BY e.department_id ORDER BY e.salary asc) drank
FROM
 hr.employees e
LEFT JOIN
 hr.departments d
ON
 e.department_id=d.department_id 
WHERE
 d.department_name = 'Human Resources' or d.department_name = 'Purchasing';

--3. Select the 3 employees with minimum salary for department id 50.
SELECT * FROM
    (SELECT
    first_name, department_id, salary, dense_rank () over (order by salary asc) drank 
    FROM
    hr.employees where department_id =50) where drank in (1,2,3);

--4. Show first name, last name, salary and previously listed employee’s salary who works in
--“IT_PROG” over hire date.


SELECT
    first_name, last_name,salary,lag(SALARY,1,0) over(order by salary)
    FROM
    hr.employees
    WHERE
    job_id='IT_PROG';

---5 Display details of current job for employees who worked as IT Programmers in the past.
SELECT e.employee_id, e.first_name, e.last_name, j.job_title, department_id
FROM hr.employees e
JOIN hr.jobs j ON e.job_id = j.job_id
WHERE e.employee_id IN (
  SELECT employee_id
  FROM hr.job_history
  WHERE job_id = 'IT_PROG'
);

---6 Make a copy of the employees table and update the salaries of the employees in the new table with the maximum salary in their departments.

create table employees1
as 
select * from hr.employees

update employees1 e1 set salary=(select max(salary) from hr.employees e where e1.department_id=e.department_id)

select * from employees1

--7. Make a copy of the employees table and update the salaries of the employees in the new table
--with a 30 percent increase.

Create Table 
    employees2 as (select * from hr.employees );
  Update employees2 set salary=1.3 * salary;
select * from employees2

8 --- First Value
SELECT
department_id, last_name, salary,
FIRST_VALUE (last_name)
OVER (partition by department_id ORDER BY salary desc) AS lowest_sal
FROM hr.employees

9--- Last Value
SELECT
last_name, salary, hire_date, department_id,
LAST_VALUE(hire_date)
OVER (partition by department_id ORDER BY salary) as lowest_hd
FROM hr.employees
