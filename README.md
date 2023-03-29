CREATE DATABASE employees_info; 
use employees_info;
CREATE TABLE employees (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  age INT,
  department_id INT
);

INSERT INTO employees (id, name, age, department_id) VALUES
  (1, 'Alice', 25, 1),
  (2, 'Bob', 30, 2),
  (3, 'Charlie', 35, 2),
  (4, 'David', 40, 3),
  (5, 'Eve', 45, 3),
  (6, 'Frank', 50, 3);
  
  -- departments table
  CREATE TABLE departments (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);

INSERT INTO departments (id, name) VALUES
  (1, 'Sales'),
  (2, 'Marketing'),
  (3, 'Engineering');
  
  SELECT name, age FROM employees;
  SELECT employees.name, departments.name AS department_name
FROM employees
JOIN departments ON employees.department_id = departments.id;

SELECT employees.name, employees.age
FROM employees
JOIN departments ON employees.department_id = departments.id
WHERE departments.name = 'Engineering';

SELECT departments.name, COUNT(employees.id) AS num_employees
FROM departments
LEFT JOIN employees ON departments.id = employees.department_id
GROUP BY departments.name;

SELECT employees.name
FROM employees
JOIN departments ON employees.department_id = departments.id
WHERE departments.name = (
  SELECT departments.name
  FROM employees
  JOIN departments ON employees.department_id = departments.id
  WHERE employees.name = 'Charlie'
);

SELECT name, age FROM employees WHERE age > 35;

SELECT employees.name, employees.age
FROM employees
JOIN departments ON employees.department_id = departments.id
WHERE departments.name IN ('Sales', 'Marketing');

SELECT employees.name, employees.age
FROM employees
JOIN departments ON employees.department_id = departments.id
WHERE departments.name = 'Engineering' AND employees.age > 40;

SELECT departments.name, COUNT(employees.id) AS num_employees
FROM departments
LEFT JOIN employees ON departments.id = employees.department_id
GROUP BY departments.name
ORDER BY num_employees DESC;

SELECT employees.name, employees.age
FROM employees
JOIN departments ON employees.department_id = departments.id
WHERE employees.age < 35 AND departments.name = (
SELECT departments.name= 'marketing'
  FROM employees
  JOIN departments  ON employees.department_id = departments.id
  WHERE employees.name = 'Bob'
);
