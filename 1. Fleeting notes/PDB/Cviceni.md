Bemp = BlockSize / RowAvg
Pemp = Nemp / BlockSize
I(EMP, EMPNO) = log(V(Emp, EmpNo)) / log(Fi) = log 30000 / log 100 = 4.5 / 2 = 2.2 = 3

Bdept = 40
Pdep = 3
I(DEPT, DeptNo) = log 100 / log 100 = 1

SELECT * FROM EMP WHERE EMPNO = 745
1. bez indexu: Full table scan = pocet blocku = 500
2. Hloubka stromu + 1 = 3 + 1 = 4

SELECT * FROM EMP WHERE EMPNO > 745
1. bez indexu: Full table scan = pocet blocku = 500
2. s indexem: Hloubka stromu +  = 3 + 1 = 4