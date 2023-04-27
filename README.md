# PL-SQL-Cheat-sheet

## ¿Que es PL SQL?

PL/SQL es una combinación de SQL junto con las características procedimentales de los lenguajes de programación. Fue desarrollado por Oracle Corporation a principios de los 90 para mejorar las capacidades de SQL. PL/SQL es uno de los tres lenguajes de programación clave integrados en la base de datos Oracle, junto con el propio SQL y Java. Este tutorial le dará una gran comprensión de PL/SQL para proceder con la base de datos Oracle y otros conceptos avanzados de RDBMS.

## Bloques en PL SQL 

Un bloque PL/SQL es un conjunto de sentencias que se agrupan en una unidad lógica. La estructura general de un bloque PL/SQL consta de tres secciones principales: declaración, ejecución y excepción.

```
DECLARE
   emp_name VARCHAR2(50) := 'John Smith';
   emp_salary NUMBER(8,2) := 5000;
   annual_salary NUMBER(8,2);
BEGIN
   annual_salary := emp_salary * 12;
   DBMS_OUTPUT.PUT_LINE(emp_name || ' earns ' || annual_salary || ' per year.');
EXCEPTION
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Error: ' || SQLCODE || ' - ' || SQLERRM);
END;

```

En la sección de declaración, se declaran las variables y constantes que se utilizarán en el bloque. En este ejemplo, se declaran dos variables: emp_name y emp_salary.

En la sección de ejecución, se colocan las sentencias que realizan las operaciones necesarias. En este ejemplo, se calcula el salario anual del empleado multiplicando su salario mensual por 12.

En la sección de excepción, se manejan las excepciones que pueden ocurrir durante la ejecución del bloque. En este ejemplo, se captura cualquier excepción y se muestra un mensaje de error en la salida estándar.En la sección de declaración, se declaran las variables y constantes que se utilizarán en el bloque. En este ejemplo, se declaran dos variables: emp_name y emp_salary.

En la sección de ejecución, se colocan las sentencias que realizan las operaciones necesarias. En este ejemplo, se calcula el salario anual del empleado multiplicando su salario mensual por 12.

En la sección de excepción, se manejan las excepciones que pueden ocurrir durante la ejecución del bloque. En este ejemplo, se captura cualquier excepción y se muestra un mensaje de error en la salida estándar.

[Miro](https://miro.com/app/board/uXjVMOF4FTM=/?share_link_id=934150606948)
