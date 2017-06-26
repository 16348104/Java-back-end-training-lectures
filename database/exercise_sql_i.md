# 附: SQL 练习题

## DDL 学生选课系统

- 学生表
 - id
 - name
 - age
 - gender
 - dob
 - departmentId
 
- 系别表
 - id
 - title `系名称`
 - tel
 
- 课程表
 - id
 - title `课程名称`
 - credit `学分`

- 选课表  
 - id
 - studentId
 - departmentId
 - grade `考试成绩`


## Sample database structure

> Table `emp` 员工表

Field    | Type        | Null | Key | Default | Comment
----------|-------------|------|-----|---------|-------
EMPNO    | int(4)      | NO   | PRI | NULL    | 员工编号
ENAME    | varchar(10) | YES  |     | NULL    | 员工姓名
JOB      | varchar(9)  | YES  |     | NULL    | 工作工种
MGR      | int(4)      | YES  |     | NULL    | 经理编号
HIREDATE | date        | YES  |     | NULL    | 入职日期
SAL      | double(7,2) | YES  |     | NULL    | 基本工资
COMM     | double(7,2) | YES  |     | NULL    | 奖金
DEPTNO   | int(2)      | YES  | MUL | NULL    | 部门编号

> Table `dept` 部门表

Field  | Type        | Null | Key | Default | Comment
--------|-------------|------|-----|---------|-------
DEPTNO | int(2)      | NO   | PRI | NULL    | 部门编号
DNAME  | varchar(14) | YES  |     | NULL    | 部门名称
LOC    | varchar(13) | YES  |     | NULL    | 所在地区

> Table `salgrade` 工资级别表

Field | Type    | Null | Key | Default | Comment
-------|---------|------|-----|---------|-------
GRADE | int(11) | YES  |     | NULL    | 工资级别
LOSAL | int(11) | YES  |     | NULL    | 最低工资
HISAL | int(11) | YES  |     | NULL    | 最高工资


> 工资 = 基本工资 + 奖金

## PART I

- \# 1. 查找部门 30 中员工的详细信息

```sql
SELECT *
FROM scott.emp
WHERE DEPTNO = 30;
```

- \# 2. 找出从事 clerk 工作的员工的编号、姓名、部门号

```sql
SELECT
  EMPNO,
  ENAME,
  DEPTNO
FROM scott.emp
WHERE JOB = 'clerk';
```

- \# 3. 检索出奖金多于基本工资的员工信息

```sql
SELECT *
FROM scott.emp
WHERE COMM > SAL;
```

- \# 4. 检索出奖金多于基本工资 30% 员工信息

```sql
SELECT *
FROM scott.emp
WHERE COMM > SAL * 0.3;
```

- \# 5. 希望看到 10 部门的经理或者 20 部门的职员 clerk 的信息

```sql
SELECT *
FROM scott.emp
WHERE ((DEPTNO = 10) AND (JOB = 'manager')) OR ((DEPTNO = 20) AND (JOB = 'clerk'));
```

- \# 6. 找出 10 部门的经理、20 部门的职员或者既不是经理也不是职员但是高于 2000 元的员工信息

```sql
SELECT *
FROM scott.emp
WHERE
  ((DEPTNO = 10) AND (JOB = 'manager'))
  OR
  ((DEPTNO = 20) AND (JOB = 'clerk'))
  OR
  ((JOB NOT IN ('manager', 'clerk')) AND (SAL + ifnull(COMM, 0) > 2000));
```

- \# 7. 找出获得奖金的员工的工作

```sql
SELECT DISTINCT JOB
FROM scott.emp
WHERE COMM > 0;
```

- \# 8. 找出奖金少于 100 或者没有获得奖金的员工的信息

```sql
SELECT *
FROM scott.emp
WHERE COMM < 100 OR COMM IS NULL;
```

- \# 9. 查找员工雇佣日期是当月的最后一天的员工信息

```sql
SELECT *
FROM scott.emp
WHERE HIREDATE = last_day(HIREDATE);
```

- \# 10. 检索出雇佣年限超过 35 年的员工信息

```sql
SELECT *
FROM scott.emp
WHERE date_add(HIREDATE, INTERVAL 35 YEAR) < current_date;
```

- \# 11. 找出姓名以 A、B、S 开始的员工信息

```sql
SELECT *
FROM scott.emp
WHERE ENAME REGEXP '^[abs]';
-- WHERE ENAME LIKE 'a%' OR emp.ENAME LIKE 'b%';
-- WHERE substr(ENAME, 1, 1) IN ('a', 'b', 's');
```

- \# 12. 找到名字长度为 4 个字符的员工信息

```sql
SELECT *
FROM scott.emp
WHERE length(ENAME) = 4;
```

- \# 13. 名字中不包含 R 字符的员工信息

```sql
SELECT *
FROM scott.emp
WHERE ENAME REGEXP '[^r]'; -- ?
-- WHERE ENAME NOT LIKE '%r%';
```

- \# 14. 找出员工名字的前3个字符

```sql
SELECT substr(ENAME, 1, 3)
FROM scott.emp;
```

- \# 15. 将名字中 A 改为 a

```sql
SELECT replace(ENAME, 'A', 'a')
FROM scott.emp;
```

- \# 16. 将员工的雇佣日期拖后 10 年

```sql
SELECT date_add(HIREDATE, INTERVAL 10 YEAR)
FROM scott.emp;
```

- \# 17. 返回员工的详细信息并按姓名排序

```sql
SELECT *
FROM scott.emp
ORDER BY ENAME;
```

- \# 18. 返回员工的信息并按员工的工作年限降序排列

```sql
SELECT *
FROM scott.emp
ORDER BY HIREDATE;
```

- \# 19. 返回员工的信息并按工作降序、工资升序排列

```sql
SELECT *
FROM scott.emp
ORDER BY JOB DESC, (SAL + ifnull(COMM, 0));
```

- \# 20. 返回员工的姓名、雇佣年份和月份，并按月份和雇佣日期排序

```sql
SELECT
  ENAME,
  year(HIREDATE),
  month(HIREDATE),
  day(HIREDATE)
FROM scott.emp
ORDER BY 3, day(HIREDATE);
```

- \# 21. 计算员工的日薪，每月按 30 天

```sql
SELECT
  ENAME,
  round((SAL + ifnull(COMM, 0)) / 30, 2)
FROM scott.emp;
```

- \# 22. 找出 2 月份雇佣的员工

```sql
SELECT *
FROM scott.emp
WHERE month(HIREDATE) = 2;
```

- \# 23. 至今为止，员工被雇佣的天数

```sql
SELECT
  hiredate,
  datediff(now(), HIREDATE)
FROM scott.emp;
```

- \# 24. 找出姓名中包含 A 的员工信息

```sql
SELECT *
FROM scott.emp
WHERE ENAME REGEXP 'a';
```

- \# 25. 计算出员工被雇佣了多少年、多少月、多少日

```sql
UPDATE scott.emp
SET HIREDATE = '2016-12-1'
WHERE ENAME = '斯科特';

SELECT
  ename,
  HIREDATE,
  TIMESTAMPDIFF(
      YEAR,
      hiredate,
      CURDATE()
  ) AS years,
  TIMESTAMPDIFF(
      MONTH,
      DATE_ADD(
          hiredate,
          INTERVAL TIMESTAMPDIFF(YEAR, hiredate, CURDATE()) YEAR
      ),
      CURDATE()
  ) AS months,
  TIMESTAMPDIFF(
      DAY,
      DATE_ADD(
          DATE_ADD(
              hiredate,
              INTERVAL TIMESTAMPDIFF(YEAR, hiredate, CURDATE()
              ) YEAR),
          INTERVAL TIMESTAMPDIFF(
              MONTH,
              DATE_ADD(
                  hiredate,
                  INTERVAL TIMESTAMPDIFF(YEAR, hiredate, CURDATE()) YEAR
              ),
              CURDATE()
          ) MONTH
      ),
      CURDATE()
  ) AS days
FROM scott.emp;
```

## PART II

- \# 1. 返回拥有员工的部门名、部门号

```sql
SELECT DISTINCT
  d.DEPTNO,
  d.DNAME
FROM scott.dept d
  JOIN scott.emp e
    ON d.DEPTNO = e.DEPTNO;
```

- \# 2. 工资多于 scott 的员工信息

```sql
SELECT *
FROM scott.emp
WHERE SAL + ifnull(COMM, 0) > (
  SELECT SAL + ifnull(COMM, 0)
  FROM scott.emp
  WHERE ENAME = 'scott'
); -- 子查询

SELECT e1.*
FROM scott.emp e1
  JOIN scott.emp e2
    ON e1.SAL + ifnull(e1.COMM, 0) > e2.SAL + ifnull(e2.COMM, 0)
WHERE e2.ENAME = 'scott'; -- 自连接 推荐

```

- \# 3. 返回员工和所属经理的姓名

```sql
SELECT
  e1.ENAME,
  e2.ENAME
FROM scott.emp e1
  JOIN scott.emp e2
    ON e1.MGR = e2.EMPNO;

SELECT
  e.ENAME,
  d.DNAME
FROM scott.emp e
  LEFT JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO; -- 外联接
```

- \# 4. 返回雇员的雇佣日期早于其经理雇佣日期的员工及其经理姓名

```sql
SELECT
  e1.ENAME,
  e2.ENAME
FROM scott.emp e1
  JOIN scott.emp e2
    ON e1.MGR = e2.EMPNO
WHERE e1.HIREDATE < e2.HIREDATE;
```

- \# 5. 返回员工姓名及其所在的部门名称

```sql
SELECT
  e.ENAME,
  d.DNAME
FROM scott.emp e
  LEFT JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO;
```

- \# 6. 返回从事 clerk 工作的员工姓名和所在部门名称

```sql
SELECT
  e.ENAME,
  d.DNAME
FROM scott.emp e
  LEFT JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO
WHERE e.JOB = 'clerk';
```

- \# 7. 返回部门号及其本部门的最低工资

```sql
SELECT
  DEPTNO,
  min(SAL + ifnull(COMM, 0))
FROM scott.emp
GROUP BY DEPTNO;
```

- \# 8. 返回销售部 sales 所有员工的姓名

```sql
SELECT ENAME
FROM scott.emp
WHERE DEPTNO = (
  SELECT DEPTNO
  FROM scott.dept
  WHERE DNAME = 'sales'
);

SELECT e.ENAME
FROM scott.emp e
  JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO
WHERE d.DNAME = 'sales';
```

- \# 9. 返回工资多于平均工资的员工

```sql
SELECT *
FROM scott.emp
WHERE sal + ifnull(COMM, 0) > (
  SELECT avg(sal + ifnull(COMM, 0))
  FROM scott.emp
);
```

- \# 10. 返回与 scott 从事相同工作的员工

```sql
SELECT e1.*
FROM scott.emp e1
  JOIN scott.emp e2
    ON e1.JOB = e2.job
WHERE e2.ENAME = 'scott';
```

- \# 11. 返回比 30 部门员工平均工资高的员工姓名与工资

```sql
SELECT
  ENAME,
  sal + ifnull(COMM, 0)
FROM scott.emp
WHERE sal + ifnull(COMM, 0) > (
  SELECT avg(sal + ifnull(COMM, 0))
  FROM scott.emp
  WHERE DEPTNO = 30
);
```

- \# 12. 返回工资高于30部门所有员工工资水平的员工信息

```sql
SELECT *
FROM scott.emp
WHERE sal + ifnull(COMM, 0) > (
  SELECT max(sal + ifnull(COMM, 0))
  FROM scott.emp
  WHERE DEPTNO = 30
);
```

- \# 13. 返回部门号、部门名、部门所在位置及其每个部门的员工总数

```sql
SELECT
  d.DEPTNO,
  d.DNAME,
  d.LOC,
  count(e.EMPNO) -- not count(*) 
FROM scott.emp e RIGHT JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO
GROUP BY d.DEPTNO;
```

- \# 14. 返回员工的姓名、所在部门名及其工资

```sql
SELECT
  e.ENAME,
  d.DNAME,
  e.SAL + ifnull(e.COMM, 0) 工资
FROM scott.emp e
  JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO;
```

- \# 15. 返回雇员表中不在同一部门但是从事相同工作的员工信息

```sql
SELECT
  e1.*,
  e2.*
FROM scott.emp e1
  JOIN scott.emp e2
    ON e1.DEPTNO <> e2.DEPTNO AND e1.JOB = e2.JOB;
```

- \# 16. 返回员工的详细信息，包括部门名

```sql
SELECT
  e.*,
  d.DNAME
FROM scott.emp e
  JOIN scott.dept d
    ON e.DEPTNO = d.DEPTNO;
```

- \# 17. 返回员工工作及其从事此工作的最低工资

```sql
SELECT
  JOB,
  min(SAL + ifnull(COMM, 0))
FROM scott.emp
GROUP BY JOB;
```

- \# 18. 返回不同部门经理的最低工资

```sql
SELECT
  DEPTNO,
  min(sal + ifnull(COMM, 0))
FROM scott.emp
WHERE JOB = 'manager'
GROUP BY DEPTNO;
```

- \# 19. 计算出员工的年薪，并且以年薪排序

```sql
SELECT (SAL + ifnull(COMM, 0)) * 12 年薪
FROM scott.emp
ORDER BY 1 DESC;
```

- \# 20. 返回工资处于第 4 级别的员工的姓名

```sql
SELECT
  e.ENAME,
  e.SAL + ifnull(COMM, 0),
  s.LOSAL,
  s.HISAL
FROM scott.emp e
  JOIN scott.salgrade s
    ON e.SAL + ifnull(COMM, 0) BETWEEN s.LOSAL AND s.HISAL
WHERE s.GRADE = 4;
```
