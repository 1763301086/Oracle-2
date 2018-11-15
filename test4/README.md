# 实验4：对象管理
## 实验1：.查询某个员工的信息
```sql
select * from ORDERS where  order_id=1;
select * from ORDER_DETAILS where  order_id=1;
select * from VIEW_ORDER_DETAILS where order_id=1;
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_1_1.png) 
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_1_2.png) 
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_1_3.png) 
## 实验2：.递归查询某个员工及其所有下属，子下属员工
```sql
WITH A (EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID) AS
  (SELECT EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID
    FROM employees WHERE employee_ID = 11
    UNION ALL
  SELECT B.EMPLOYEE_ID,B.NAME,B.EMAIL,B.PHONE_NUMBER,B.HIRE_DATE,B.SALARY,B.MANAGER_ID,B.DEPARTMENT_ID
    FROM A, employees B WHERE A.EMPLOYEE_ID = B.MANAGER_ID)
SELECT * FROM A;
--或者
SELECT * FROM employees START WITH EMPLOYEE_ID = 11 CONNECT BY PRIOR EMPLOYEE_ID = MANAGER_ID;
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_2.png)  
## 实验3：.查询订单表，并且包括订单的订单应收货款: Trade_Receivable= sum(订单详单表.ProductNum*订单详单表.ProductPrice)- Discount
```sql
select a.*,(select sum(b.product_num*b.product_price)
from order_details b
where b.order_id=c.order_id
group by b.order_id)-a.discount as "应收货款"
from orders a,order_details c
where a.order_id=c.order_id;
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_3.png) 
## 实验4：.查询订单详表，要求显示订单的客户名称和客户电话，产品类型用汉字描述
```sql
select CUSTOMER_NAME,CUSTOMER_TEL,PRODUCT_TYPE from ORDERS,PRODUCTS where 
exists (select ORDERS_ID,PRODUCT_NAME from ORDERS_DETAILS);
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_4.png) 
## 实验5：.查询出所有空订单，即没有订单详单的订单
```sql
select orders.*
from orders a left join order_details b
on a.order_id=b.order_id
where b.order_id is null
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_5.png) 
## 实验6.查询部门表，同时显示部门的负责人姓名
```sql
select departments.*,employees.name as "负责人"
from departments,employees
where departments.department_id=employees.department_id
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_6.png) 
## 实验7.查询部门表，统计每个部门的销售总金额
```sql
select department_name ,sum(all_money) as "部门总销售额"
from(
select sum(c.Trade_Receivable) as all_money,c.employee_id,b.department_id,a.department_name
from departments a,employees b,orders c 
where a.department_id=b.department_id
and b.employee_id=c.employee_id
group by c.employee_id,b.department_id,a.department_name
)
group by department_id,department_name
```
![](https://github.com/YangTingGet/Oracle/blob/master/test4/%E5%AE%9E%E9%AA%8C4_7.png) 
