##查询1：
```
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
##查询2：
```
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```
![](https://github.com/YangTingGet/Oracle/blob/master/test1/111.png)
![](https://github.com/YangTingGet/Oracle/blob/master/test1/QQ%E6%88%AA%E5%9B%BE20181018225257.png)
![](https://github.com/YangTingGet/Oracle/blob/master/test1/QQ%E6%88%AA%E5%9B%BE20181018225156.png)

##自己的实验：
```
SELECT  d.department_name as "部门",e.FIRST_NAME as 姓名 ,e.SALARY as 工资
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_idz
and e.SALARY>6000
```
