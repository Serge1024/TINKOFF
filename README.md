
CREATE TABLE Jobtitles (
  jobtitle_id INT PRIMARY KEY,
  name VARCHAR(100)
);

-- Insert sample data into Employees table
INSERT INTO Jobtitles (jobtitle_id, name) VALUES
  (1, 'Разработчик'),
  (2, 'Системный аналитик'),
  (3, 'Менеджер проектов'),
  (4, 'Системный администратор'),
  (5, 'Руководитель группы'),
  (6, 'Инженер тестирования'),
  (7, 'Сотрудник группы поддержки');

Select * from Jobtitles;

CREATE TABLE Staff (
  staff_id INTEGER,
  name TEXT,
  salary INTEGER,
  email TEXT, 
  birthday DATE, 
  jobtitle_id INTEGER
);

INSERT INTO Staff (staff_id, name, salary, email, birthday, jobtitle_id) VALUES
  (1, 'Иванов Сергей', 100000, 'test@test.ru', '03.03.1990', 1),
  (2, 'Петров Пётр', 60000, 'petr@test.ru', '12.01.2000', 7),
  (3, 'Сидоров Василий', 80000, 'test@test.ru', '02.04.1999', 6),
  (4, 'Максимов Иван', 70000, 'ivan.m@test.ru', '10.02.1997', 4),
  (5, 'Попов Иван', 120000, 'popov@test.ru', '04.25.2001', 5);

----------111111
select email
from
  staff
group by
  1
having count(1) > 1;


----------222222
select staff_id
  , EXTRACT(day from now() - birthday) / 365 as years_old
from 
  staff;
  

--------------3
select name
from
  Jobtitles
where jobtitle_id = 
  (select jobtitle_id
  from
    staff
  order by
    salary
    desc
  offset 1 ROWS
  fetch next 1 ROWS ONLY)
