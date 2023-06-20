### 1.- Bloqueos y transacciones 

Mecanismos de las bases de datos para poder manejar los accesos concurrentes de las bases de datos.
Para evitar que dos personas editen los valores al mismo tiempo.

Exiten dos tipos de Bloqueos

#### SHARED BLOCK
Bloqueos compartidos
Nadie puede escribir, pero todos pueden leer

#### RESERVED BLOCK
Se aplica cuando estamos escribiendo en la base de datos se bloquea. Permitiendo leer pero no escribir

#### BLOQUEO EXCLUSIVO

Permite bloquear la escritura y leectura a todos los usuarios

    UPDATE Products SET ProductName = 'Tazon' WHERE ProductName = 'Chais';
    COMMIT;

Con COMMIT asentamos los cambios

Cambio de valor

    UPDATE Products SET ProductName = 'Tazon' WHERE ProductName = 'Chais';
    ROLLBACK;

Rollback nos permite retroceder cambios siempre y cuando no se realice el COMMIT

### 2.- Procedimientos almacenados

Es como un conjunto de instrucciones guardados en la base de datos que podemos utilizar en cualquier momento.

### 3.- Funciones definidas por el usuario
[ejercicio en python](././Python/UDF.ipynb)

### 4.- Ejercicio final (SQL + Python)
[Ejercicio Final](./Python/Rent.ipynb)

### 5.- Diferencias con otros DBMS
#### Diferencias entre Caracteristicas
**SQLite** es una base de datos de motor ligero y del archivo único un único.

no utiliza un proceso de servidor dedicado.

Simple es ideal para aplicaciones que son incrustadas y también de prototipos no es apropiado para aplicaciones de
Gran escala.

**MySQL** bases de datos basado en servidor.

sqlite por ejemplo soportaba un solo conjunto de sql mientras que mysql soporta varios y es ideal para aplicaciones de Gran escala o sea es excelente para esto 

**PostGress** también es un gestor de base de datos basado en en servidor soporta también un conjunto completo de características de sql y también tiene sus propias extensiones y también es ideal para aplicaciones web para proyectos empresariales y para escalar y 

Después **sql server** también
basado en servidor obviamente es de Microsoft de pago también soporte un conjunto completo de características de sql y También incluye como pobre extensiones propias es ideal para aplicaciones de Gran escala

#### Código
Crear una Tabla
lo unico que cambia es en MySQL agregar el motor de almacenamiento.
![Crear Tablas](./../img/Captura%20de%20pantalla%20(171).png)

Trabajar con claves primarias en diferente.
![Claves primarias](./../img/Captura%20de%20pantalla%20(172).png)

INNER
Rigth join es diferente.
![Right JOIN](./../img/Captura%20de%20pantalla%20(173).png)

FULL JOIN 
Tambien es diferente.
![FULL JOIN](./../img/Captura%20de%20pantalla%20(174).png)

Funciones de agregación son iguales.

Los indices tambien son iguales, al iguales que las transacciones.

NOW para la fecha puede variar
![NOW](./../img/Captura%20de%20pantalla%20(176).png)

    Round es igual. redondea dependiendo.
    Ceil, Ceiling, Redondea para arriba.
    Floor, para abajo

Limit tambien varia para SQL server
![Claves primarias](./../img/Captura%20de%20pantalla%20(178).png)

Para ofset se usa diferente en SQL server
![Claves primarias](./../img/Captura%20de%20pantalla%20(179).png)


### 6.- Escena Final