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

### Declaraiones

La sintaxis para declarar una variable es:

```
variable_name [CONSTANT] datatype [NOT NULL] [:= | DEFAULT initial_value]
```

Donde, variable_name es un identificador válido en PL/SQL, datatype debe ser un tipo de dato válido en PL/SQL . Algunas declaraciones de variables válidas junto con su definición se muestran a continuación:

```
sales number(10, 2);
pi CONSTANT double precision := 3.1415;
name varchar2(25);
address varchar2(100);
```

Cuando se establece un límite de tamaño, escala o precisión con el tipo de dato, se habla de declaración restringida. Por ejemplo:

```
sales number(10, 2);
name varchar2(25);
address varchar2(100);
```

### Iniacializacion de variables

Siempre que se declara una variable, PL/SQL le asigna un valor por defecto de NULL. Si desea inicializar una variable con un valor distinto del valor NULL, puede hacerlo durante la declaración, utilizando cualquiera de las siguientes opciones:

<ul>
   <li>DEFAULT</li>
   <li>Una asiganición con ":="</li>
</ul>

```
counter binary_integer := 0;
greetings varchar2(20) DEFAULT 'Have a Good Day';
```
Nota: Por recomendación asignar un valor a la hora de inicializar una variable

De igual forma se puede hacer la declaración de la restricción NOT NULL para espcificar que la variable no debería ser NULL.

## Alcance de las variables

PL/SQL permite el anidamiento de bloques, es decir, cada bloque de programa puede contener otro bloque interior. Si una variable se declara dentro de un bloque interno, no es accesible para el bloque externo. Sin embargo, si una variable se declara y es accesible para un bloque externo, también será accesible para todos los bloques internos anidados. Existen dos tipos de ámbito de las variables:

***Variables locales-*** Variables declaradas en un bloque interno y no accesibles a bloques externos.
***Variables Globales-*** Variables declaradas en el bloque más externo o en un paquete.

```
DECLARE
 -- Global variables
   num1 number := 95;
   num2 number := 85;
BEGIN
   dbms_output.put_line('Outer Variable num1: ' || num1);
   dbms_output.put_line('Outer Variable num2: ' || num2);
   DECLARE
      -- Local variables
      num1 number := 195;
      num2 number := 185;
   BEGIN
      dbms_output.put_line('Inner Variable num1: ' || num1);
      dbms_output.put_line('Inner Variable num2: ' || num2);
   END;
END;
/
```

## Asignación de resultados de consultas SQL a variables PL/SQL
Puede utilizar la sentencia SELECT INTO de SQL para asignar valores a variables PL/SQL. Para cada elemento de la lista SELECT, debe haber una variable correspondiente y compatible con el tipo en la lista INTO. El siguiente ejemplo ilustra el concepto. Creemos una tabla llamada CLIENTES -

```
CREATE TABLE CUSTOMERS(
 ID   INT NOT NULL,
   NAME VARCHAR (20) NOT NULL,
   AGE INT NOT NULL,
   ADDRESS CHAR (25),
   SALARY   DECIMAL (18, 2),
   PRIMARY KEY (ID)
);
```
```
INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (1, 'Ramesh', 32, 'Ahmedabad', 2000.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (2, 'Khilan', 25, 'Delhi', 1500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (3, 'kaushik', 23, 'Kota', 2000.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (4, 'Chaitali', 25, 'Mumbai', 6500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (5, 'Hardik', 27, 'Bhopal', 8500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (6, 'Komal', 22, 'MP', 4500.00 );
```
```
DECLARE
 c_id customers.id%type := 1;
   c_name  customers.name%type;
   c_addr customers.address%type;
   c_sal  customers.salary%type;
BEGIN
   SELECT name, address, salary INTO c_name, c_addr, c_sal
   FROM customers
   WHERE id = c_id;
   dbms_output.put_line
   ('Customer ' ||c_name || ' from ' || c_addr || ' earns ' || c_sal);
END;
/
```

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

**IF-THEN-ELSIF**

Ejemplo

```
DECLARE 
 a number(3) := 100; 
BEGIN 
   IF ( a = 10 ) THEN 
      dbms_output.put_line('Value of a is 10' ); 
   ELSIF ( a = 20 ) THEN 
      dbms_output.put_line('Value of a is 20' ); 
   ELSIF ( a = 30 ) THEN 
      dbms_output.put_line('Value of a is 30' ); 
   ELSE 
       dbms_output.put_line('None of the values is matching'); 
   END IF; 
   dbms_output.put_line('Exact value of a is: '|| a );  
END;
```

Salida

```
None of the values is matching 
Exact value of a is: 100 

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_if_then_elsif.htm)

**CASE**

Al igual que la sentencia IF, la sentencia CASE selecciona una secuencia de sentencias para su ejecución. Sin embargo, para seleccionar la secuencia, la sentencia CASE utiliza un selector en lugar de varias expresiones booleanas. Un selector es una expresión cuyo valor se utiliza para seleccionar una de varias alternativas.

Ejemplo

```
DECLARE 
 grade char(1) := 'A'; 
BEGIN 
   CASE grade 
      when 'A' then dbms_output.put_line('Excellent'); 
      when 'B' then dbms_output.put_line('Very good'); 
      when 'C' then dbms_output.put_line('Well done'); 
      when 'D' then dbms_output.put_line('You passed'); 
      when 'F' then dbms_output.put_line('Better try again'); 
      else dbms_output.put_line('No such grade'); 
   END CASE; 
END;
```

Salida

```
Excellent 

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_case_statement.htm)

**Searched CASE**

La sentencia CASE buscada no tiene selector y las cláusulas WHEN de la sentencia contienen condiciones de búsqueda que dan valores booleanos.

Ejemplo

```
DECLARE 
 grade char(1) := 'B'; 
BEGIN 
   case  
      when grade = 'A' then dbms_output.put_line('Excellent'); 
      when grade = 'B' then dbms_output.put_line('Very good'); 
      when grade = 'C' then dbms_output.put_line('Well done'); 
      when grade = 'D' then dbms_output.put_line('You passed'); 
      when grade = 'F' then dbms_output.put_line('Better try again'); 
      else dbms_output.put_line('No such grade'); 
   end case; 
END;
```

Salida 

```
Very good 

PL/SQL procedure successfully completed.

[Fuente](https://www.tutorialspoint.com/plsql/plsql_searched_case.htm)
```

### Loops

[Miro](https://miro.com/app/board/uXjVMOF4FTM=/?share_link_id=934150606948)
