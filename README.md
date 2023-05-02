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

### Inicializacion de variables

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

### Alcance de las variables

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

### Asignación de resultados de consultas SQL a variables PL/SQL
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

**Basic Loop**

La estructura básica del bucle incluye una secuencia de sentencias entre las sentencias LOOP y END LOOP. Con cada iteración, la secuencia de sentencias se ejecuta y luego el control se reanuda en la parte superior del bucle.

```
LOOP
 Sequence of statements;
END LOOP;

Veamos un ejemplo

DECLARE
 x number := 10;
BEGIN
   LOOP
      dbms_output.put_line(x);
      x := x + 10;
      IF x > 50 THEN
         exit;
      END IF;
   END LOOP;
   -- after exit, control resumes here
   dbms_output.put_line('After Exit x is: ' || x);
END;
```
Salida
```
10
20
30
40
50
After Exit x is: 60

PL/SQL procedure successfully completed.
```

Puede utilizar la sentencia EXIT WHEN en lugar de la sentencia EXIT

```
DECLARE
 x number := 10;
BEGIN
   LOOP
      dbms_output.put_line(x);
      x := x + 10;
      exit WHEN x > 50;
   END LOOP;
   -- after exit, control resumes here
   dbms_output.put_line('After Exit x is: ' || x);
END;
```
Salida
```
10
20
30
40
50
After Exit x is: 60

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_basic_loop.htm)

**WHILE LOOP**

Una sentencia WHILE LOOP en el lenguaje de programación PL/SQL ejecuta repetidamente una sentencia objetivo mientras una condición dada sea verdadera.

```
WHILE condition LOOP
 sequence_of_statements
END LOOP;
```

Ejemplo

```
DECLARE
 a number(2) := 10;
BEGIN
   WHILE a < 20 LOOP
      dbms_output.put_line('value of a: ' || a);
      a := a + 1;
   END LOOP;
END;
```

Salida

```
value of a: 10
value of a: 11
value of a: 12
value of a: 13
value of a: 14
value of a: 15
value of a: 16
value of a: 17
value of a: 18
value of a: 19

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_while_loop.htm)

**FOR LOOP**

Un BUCLE FOR es una estructura de control de repetición que le permite escribir eficientemente un bucle que necesita ejecutarse un número específico de veces.

FOR counter IN initial_value .. final_value LOOP
 sequence_of_statements;
END LOOP;

A continuación se muestra el flujo de control en un bucle For -

El paso inicial se ejecuta primero, y sólo una vez. Este paso permite declarar e inicializar cualquier variable de control del bucle.

A continuación, se evalúa la condición, es decir, valor_inicial .. valor_final. Si es TRUE, se ejecuta el cuerpo del bucle. Si es FALSE, el cuerpo del bucle no se ejecuta y el flujo de control salta a la siguiente sentencia justo después del bucle for.

Después de que el cuerpo del bucle for se ejecuta, el valor de la variable contador se incrementa o disminuye.

La condición se evalúa de nuevo. Si es TRUE, el bucle se ejecuta y el proceso se repite (cuerpo del bucle, luego paso de incremento, y luego otra vez la condición). Cuando la condición se convierte en FALSE, el bucle FOR-LOOP termina.

Las siguientes son algunas características especiales de PL/SQL para bucle -

El valor_inicial y el valor_final de la variable o contador del bucle pueden ser literales, variables o expresiones pero deben evaluarse como números. En caso contrario, PL/SQL lanza la excepción predefinida VALUE_ERROR.

No es necesario que el valor_inicial sea 1; sin embargo, el incremento (o decremento) del contador del bucle debe ser 1.

PL/SQL permite la determinación del rango del bucle dinámicamente en tiempo de ejecución.

Ejemplo
```
DECLARE
 a number(2);
BEGIN
   FOR a in 10 .. 20 LOOP
      dbms_output.put_line('value of a: ' || a);
  END LOOP;
END;
/
```
Salida
```
value of a: 10
value of a: 11
value of a: 12
value of a: 13
value of a: 14
value of a: 15
value of a: 16
value of a: 17
value of a: 18
value of a: 19
value of a: 20

PL/SQL procedure successfully completed.
```

Por defecto, la iteración procede desde el valor inicial al valor final, generalmente hacia arriba desde el límite inferior al superior. Puede invertir este orden utilizando la palabra clave REVERSE. En tal caso, la iteración procede en sentido contrario. Después de cada iteración, se decrementa el contador del bucle.

Sin embargo, debe escribir los límites de rango en orden ascendente (no descendente).
```
DECLARE
 a number(2) ;
BEGIN
   FOR a IN REVERSE 10 .. 20 LOOP
      dbms_output.put_line('value of a: ' || a);
   END LOOP;
END;
```
Salida
```
value of a: 20
value of a: 19
value of a: 18
value of a: 17
value of a: 16
value of a: 15
value of a: 14
value of a: 13
value of a: 12
value of a: 11
value of a: 10

PL/SQL procedure successfully completed.
```
[Fuente](https://www.tutorialspoint.com/plsql/plsql_for_loop.htm)

Tambien, puedes tener Loops anidados como se muestra a continuacion
```
LOOP 
 Sequence of statements1 
   LOOP 
      Sequence of statements2 
   END LOOP; 
END LOOP;

FOR counter1 IN initial_value1 .. final_value1 LOOP 
 sequence_of_statements1 
   FOR counter2 IN initial_value2 .. final_value2 LOOP 
      sequence_of_statements2 
   END LOOP; 
END LOOP;

WHILE condition1 LOOP 
 sequence_of_statements1 
   WHILE condition2 LOOP 
      sequence_of_statements2 
   END LOOP; 
END LOOP;
```

Las sentencias de control de bucle
Las sentencias de control de bucle cambian la ejecución de su secuencia normal. Cuando la ejecución abandona un ámbito, se destruyen todos los objetos automáticos que se crearon en ese ámbito.

PL/SQL soporta las siguientes sentencias de control. Etiquetar bucles también ayuda a tomar el control fuera de un bucle.

**EXIT**

```
DECLARE 
 a number(2) := 10; 
BEGIN 
   -- while loop execution  
   WHILE a < 20 LOOP 
      dbms_output.put_line ('value of a: ' || a); 
      a := a + 1; 
      IF a > 15 THEN 
         -- terminate the loop using the exit statement 
         EXIT; 
      END IF; 
   END LOOP; 
END;
```
Salida
```
value of a: 10 
value of a: 11 
value of a: 12 
value of a: 13 
value of a: 14 
value of a: 15 

PL/SQL procedure successfully completed.
```

**CONTINUE**

La sentencia CONTINUE hace que el bucle se salte el resto de su cuerpo y vuelva a probar inmediatamente su condición antes de reiterarse. En otras palabras, fuerza la siguiente iteración del bucle, saltándose cualquier código intermedio.

Ejemplo

```
DECLARE 
 a number(2) := 10; 
BEGIN 
   -- while loop execution  
   WHILE a < 20 LOOP 
      dbms_output.put_line ('value of a: ' || a); 
      a := a + 1; 
      IF a = 15 THEN 
         -- skip the loop using the CONTINUE statement 
         a := a + 1; 
         CONTINUE; 
      END IF; 
   END LOOP; 
END;
```

Salida

```
value of a: 10 
value of a: 11 
value of a: 12 
value of a: 13 
value of a: 14 
value of a: 16 
value of a: 17 
value of a: 18 
value of a: 19 

PL/SQL procedure successfully completed.
```

## Funciones



## Excepciones

Una excepción es una condición de error durante la ejecución de un programa. PL/SQL ayuda a los programadores a capturar tales condiciones usando el bloque EXCEPTION en el programa y se toma una acción apropiada contra la condición de error. Hay dos tipos de excepciones:

Excepciones definidas por el sistema
Excepciones definidas por el usuario

La sintaxis general para el manejo de excepciones es la siguiente. Aquí puede enumerar tantas excepciones como pueda manejar. La excepción predeterminada se manejará usando WHEN otros THEN:

```
DECLARE 
 <declarations section> 
BEGIN 
   <executable command(s)> 
EXCEPTION 
   <exception handling goes here > 
   WHEN exception1 THEN  
      exception1-handling-statements  
   WHEN exception2  THEN  
      exception2-handling-statements  
   WHEN exception3 THEN  
      exception3-handling-statements 
   ........ 
   WHEN others THEN 
      exception3-handling-statements 
END;
```

Ejemplo

```
DECLARE 
 c_id customers.id%type := 8; 
   c_name customerS.Name%type; 
   c_addr customers.address%type; 
BEGIN 
   SELECT  name, address INTO  c_name, c_addr 
   FROM customers 
   WHERE id = c_id;  
   DBMS_OUTPUT.PUT_LINE ('Name: '||  c_name); 
   DBMS_OUTPUT.PUT_LINE ('Address: ' || c_addr); 

EXCEPTION 
   WHEN no_data_found THEN 
      dbms_output.put_line('No such customer!'); 
   WHEN others THEN 
      dbms_output.put_line('Error!'); 
END; 
/
```

Salida

```
No such customer! 

PL/SQL procedure successfully completed.
```
El programa anterior muestra el nombre y la dirección de un cliente cuya identificación se proporciona. Dado que no hay ningún cliente con valor de ID 8, el programa genera la excepción de tiempo de ejecución NO_DATA_FOUND, que se captura en el bloque EXCEPCIÓN.

**Raising Exceptions**

el programador puede generar excepciones explícitamente mediante el comando RAISE.

La siguiente es la sintaxis simple para generar una excepción:

```
DECLARE 
 exception_name EXCEPTION; 
BEGIN 
   IF condition THEN 
      RAISE exception_name; 
   END IF; 
EXCEPTION 
   WHEN exception_name THEN 
   statement; 
END;
```

Puede usar la sintaxis anterior para generar la excepción estándar de Oracle o cualquier excepción definida por el usuario.

**Excepciones definidas por el usuario**

PL/SQL le permite definir sus propias excepciones según la necesidad de su programa. Una excepción definida por el usuario debe declararse y luego generarse explícitamente, utilizando una instrucción RAISE o el procedimiento DBMS_STANDARD.RAISE_APPLICATION_ERROR.

La sintaxis para declarar una excepción es:

```
DECLARE 
  my-exception EXCEPTION;
```

Ejemplo

```
DECLARE 
 c_id customers.id%type := &cc_id; 
   c_name customerS.Name%type; 
   c_addr customers.address%type;  
   -- user defined exception 
   ex_invalid_id  EXCEPTION; 
BEGIN 
   IF c_id <= 0 THEN 
      RAISE ex_invalid_id; 
   ELSE 
      SELECT  name, address INTO  c_name, c_addr 
      FROM customers 
      WHERE id = c_id;
      DBMS_OUTPUT.PUT_LINE ('Name: '||  c_name);  
      DBMS_OUTPUT.PUT_LINE ('Address: ' || c_addr); 
   END IF; 

EXCEPTION 
   WHEN ex_invalid_id THEN 
      dbms_output.put_line('ID must be greater than zero!'); 
   WHEN no_data_found THEN 
      dbms_output.put_line('No such customer!'); 
   WHEN others THEN 
      dbms_output.put_line('Error!');  
END; 
/
```

Salida

```
Enter value for cc_id: -6 (let's enter a value -6) 
old 2: c_id customers.id%type := &cc_id; 
new  2: c_id customers.id%type := -6; 
ID must be greater than zero! 
 
PL/SQL procedure successfully completed.
```

**Excepciones predefinidas**

PL/SQL proporciona muchas excepciones predefinidas, que se ejecutan cuando un programa viola cualquier regla de la base de datos. Por ejemplo, la excepción predefinida NO_DATA_FOUND se genera cuando una declaración SELECT INTO no devuelve filas.

|Exception|	Oracle Error	|SQLCODE|	Description|
-------------------------------------------------------------------------------------------------------------------------------------------------------------
|ACCESS_INTO_NULL|	06530	|-6530|	It is raised when a null object is automatically assigned a value.|
|CASE_NOT_FOUND|	06592|	-6592|	It is raised when none of the choices in the WHEN clause of a CASE statement is selected, and there is no ELSE clause.|
|COLLECTION_IS_NULL|	06531|	-6531|	It is raised when a program attempts to apply collection methods other than EXISTS to an uninitialized nested table or varray, or the program attempts to assign values to the elements of an uninitialized nested table or varray.|
|DUP_VAL_ON_INDEX|	00001	|-1	|It is raised when duplicate values are attempted to be stored in a column with unique index.|
|INVALID_CURSOR|	01001	|-1001|	It is raised when attempts are made to make a cursor operation that is not allowed, such as closing an unopened cursor.|
|INVALID_NUMBER|	01722	|-1722|	It is raised when the conversion of a character string into a number fails because the string does not represent a valid number.|
|LOGIN_DENIED|	01017|	-1017|	It is raised when a program attempts to log on to the database with an invalid username or password.|
|NO_DATA_FOUND|	01403	|+100|	It is raised when a SELECT INTO statement returns no rows.|
|NOT_LOGGED_ON|	01012|	-1012|It is raised when a database call is issued without being connected to the database.|
|PROGRAM_ERROR|	06501	|-6501|	It is raised when PL/SQL has an internal problem.|
|ROWTYPE_MISMATCH|	06504	|-6504	|It is raised when a cursor fetches value in a variable having incompatible data type.|
|SELF_IS_NULL|	30625	|-30625|	It is raised when a member method is invoked, but the instance of the object type was not initialized.|
|STORAGE_ERROR|	06500|	-6500|	It is raised when PL/SQL ran out of memory or memory was corrupted.|
|TOO_MANY_ROWS|	01422|	-1422|	It is raised when a SELECT INTO statement returns more than one row.|
|VALUE_ERROR|	06502	|-6502|	It is raised when an arithmetic, conversion, truncation, or sizeconstraint error occurs.|
|ZERO_DIVIDE|	01476|	1476|	It is raised when an attempt is made to divide a number by zero.|

## Cursores de SQL



## Triggers 



## Diferencias entre los triggers  BEFORE, AFTER, e  INSTEAD OF


[Miro](https://miro.com/app/board/uXjVMOF4FTM=/?share_link_id=934150606948)
