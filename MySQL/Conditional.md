## 11-10 방과후 

### 조건문과 연산자 문제들을 풀어보았다.

--where 조건문 select A from B where C   C의 조건을 충족하는거만 가져옴--
--근무 부서가 10번인 사원들의 사원번호, 이름 ,근무 부서를 가져온다.--
select EMPNO, ENAME, DEPTNO
from EMP where DEPTNO = 10;

--근무 부서 번호가 10번이 아닌 사원들의 사원번호, 이름 ,근무 부서 번호를 가져온다.--
select EMPNO, ENAME, DEPTNO
from EMP where DEPTNO != 10;

--급여가 1500이상인 사원들의 사원번호,이름, 급여를 가져온다.--
select EMPNO,ENAME,SAL
from EMP where SAL >= 1500;

-- 이름이 SCOTT 사원의 사원번호, 이름, 직무, 급여를 가져오기 --
select EMPNO,ENAME,JOB, SAL
from EMP where ENAME = 'SCOTT';

--직무가 SALESMAN인 사원의 사원번호, 이름, 직무를 가져온다.--
select EMPNO,ENAME, JOB
from EMP where JOB = 'SALESMAN';

--직무가 CLERK이 아닌 사원의 사원번호,이름, 직무를 가져온다.--

select EMPNO,ENAME, JOB
from EMP where JOB != 'CLERK';

-- 1982년 1월 1일 이후에 입사한 사원의 사원번호, 이름, 입사일을 가져온다.
select EMPNO, ENAME, HiREDATE from EMP where HiREDATE >= '1982/01/01';

-- 논리 연산자
-- 10번 부서에서 근무하고있는 직무가 MANAGER인 사원의 사원번호, 이름, 근무부서, 직무를 가져온다.
select empno, ename, deptno,job from emp where deptno = 10 and job = 'MANAGER';

-- 입사년도가 1981년인 사원중에 급여가 1500이상인 사원의 사원번호, 이름, 급여, 입사일을 가져온다.
select empno,ename,sal,hiredate from emp where HIREDATE between '1981/01/01' and  '1981/12/31' and sal >= 1500;

-- 20번 부서에 근무하고 있는 사원중에 급여가 1500이상인 사원의 사원번호, 이름, 부서번호, 급여를 가져온다.
select empno, ename, deptno, sal from emp where deptno = 20 and sal >= 1500;

-- 직속상관 사원 번호가 7698번인 사원중에 직무가 CLERK인 사원의 사원번호, 이름, 직속상관번호, 직무를 가져온다.
select empno,ename,mgr,job from emp where mgr = 7698 and job = 'CLERK';

-- 급여가 2000보다 크거나 1000보다 작은 사원의 사원번호 이름 급여를 가져온다
select empno, ename, sal from emp where sal > 2000 or sal < 1000;
-- 부서번호가 20이거나 30인 사원의 사원번호 이름 부서번호를 자여ㅗㄴ다

select empno, ename , deptno from emp where deptno = 20 or deptno = 30; 

-- 직무가 CLERK, SALESMAN, ANAYST인 사원의 사원번호 이름 직무를 ㄱ져온다.
select empno, ename, job from emp where job = 'CLERK' or job = 'SALESMAN' or job = 'ANALYST';
-- in 써서 해보기
select empno, ename, job from emp where job in ('CLERK', 'SALESMAN', 'ANALYST');

-- 사원번호가 7499,7566,7839 가 아닌 사원들의 사원번호, 이름을 가져온다.
select empno, ename from emp where empno not in(7499, 7566, 7839);
