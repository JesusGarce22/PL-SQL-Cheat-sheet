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

## Variables y constantes


## Condicionales y loops

### Condicionales

**IF - THEN**

La sentencia IF asocia una condición con una secuencia de sentencias encerradas por las palabras clave THEN y END IF. Si la condición es TRUE, las sentencias se ejecutan, y si la condición es FALSE o NULL, la sentencia IF no hace nada

```
IF (a <= 20) THEN
 c:= c+1;
END IF;
```

Veamos un ejemplo

```
DECLARE
 a number(2) := 10;
BEGIN
   a:= 10;
  -- check the boolean condition using if statement
   IF( a < 20 ) THEN
      -- if condition is true then print the following
      dbms_output.put_line('a is less than 20 ' );
   END IF;
   dbms_output.put_line('value of a is : ' || a);
END;
```

Cuando el código anterior se ejecuta en el prompt SQL, produce el siguiente resultado

```
a is less than 20
value of a is : 10

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_if_then.htm)

**IF-THEN-ELSE**

Este condicional nos permite agragar una accion para que se ejecute si la condicion no se cumple

Ejemplo

```
DECLARE
 a number(3) := 100;
BEGIN
   -- check the boolean condition using if statement
   IF( a < 20 ) THEN
      -- if condition is true then print the following
      dbms_output.put_line('a is less than 20 ' );
   ELSE
      dbms_output.put_line('a is not less than 20 ' );
   END IF;
   dbms_output.put_line('value of a is : ' || a);
END;
```

Resultado

```
a is not less than 20
value of a is : 100

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_if_then_else.htm)



[Miro](https://miro.com/app/board/uXjVMOF4FTM=/?share_link_id=934150606948)
