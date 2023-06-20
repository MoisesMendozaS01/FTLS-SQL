###   1. FUNCIONES DE AGREGACIÓN
Función de agregación **COUNT**

    SELECT count(FirstName) FROM Employees

Count me entrega la cantidad de datos en FirstName y me crea una nueva columna de resultado llamada FirstName.

    SELECT count(FirstName) as Cantidad_de_nombres FROM Employees

De esta manera le colocamos el nombre que queramos.

    SELECT SUM(Price) FROM Products

**SUM** me suma los valores de la columna

    SELECT AVG(Price) FROM Products

**AVG** Me arroja el promedio de todos los valores

    SELECT round(AVG(Price)) FROM Products

**Round** Me redondea el valor

SELECT round(AVG(Price),4) FROM Products

**Round** Me redondea el valor con cuatro digitos

    SELECT MIN(Price) FROM Products

**MIN** Me arroja el precio mas bajo

    SELECT ProductName, MIN(Price) FROM Products
    WHERE ProductName is NOT NULL

En este ejemplo traemos tambien el nombre del producto, donde el nombre del producto no sea null

**MAX** Valor máximo

### 2. Comentarios 

    --Comentario que no se ejecuta
    SELECT ProductName, MIN(Price) FROM Products
    WHERE ProductName is NOT NULL


### 3. GROUP BY y HAVING

    SELECT SupplierID,AVG(Price) as promedio FROM Products 
    Group by SupplierID 
    Order by promedio desc

**ORDER BY** no agrupa por SuplierID y lo promedia

    SELECT SupplierID,round(AVG(Price)) as promedio FROM Products 
    Group by SupplierID 
    HAVING promedio > 40

**HAVING** Filtra por grupos y se escribe después a diferencia de **WHERE** que nos filtra por registro

    SELECT SupplierID,round(AVG(Price)) as promedio FROM Products 
    where ProductName IS NOT NULL
    Group by SupplierID 
    HAVING promedio > 40

Aqui filtramos los valores que contienen null para que no se tomen en cuenta.

    SELECT ProductID, sum(Quantity)as total from OrderDetails
    GROUP by ProductID
    ORDER BY total
    LIMIT 1

Con este código obtenermos todos los productos que se venden con su cantidad, sumamos las cantidades vendidas pero agrupadas por su productID ordenadas por el que tiene menos ventas
Si deseamos ver solo el valor con menos ventas podemos usar **LIMIT**

    No podemos mezclar funciones de agregación con otras funciones de agregación.

### **Jerarquia de as consultas**
    1.- Seleccionamos el registro
    2.- Filtramos los registros con WHERE
    3.- Aplicamos condiciones de agrupaciones por ejemplo groupby
    4.- Podemos aplicar having que solo se puede aplicar a grupos
    5.- Ordenamientos
    6.- Limites

### 4. Subconsultas (subqueries)

Las subconsultas nos permiten unir tablas.

Si queremos saber que productos se vendieron y que precio se vendieron para saber que producto tuvo mejores ventas.

Las subconsulta no es la mejor manera para relacionar las tablas pero fueron la base que despues reemplazaron los **JOIN**.

    SELECT 	ProductID,
		Quantity, 
		(SELECT ProductName from Products),
		(SELECT CategoryID from Products) 
    FROM OrderDetails

Se coloca entre parentesis la nueva subconsulta para que nos agregue una nueva columna de valores, si deseamos agregar otra columna con otro valor debemos agregar la fuera de esta parentesis

Sin embargo en cada fila obtendra todos los valores de la subconsulta en la columna final, dejando siempre solo el primero, repitiendose con todos, por lo que tenemos que filtrar para que se asigne el nombre a cada uno como corresponda.

    SELECT 	ProductID,
		Quantity, 
		(SELECT ProductName from Products  where OrderDetails.ProductID = ProductID) as Name
    FROM OrderDetails

Ahora si los relacionasmo de la tabla orderDetail.ProductID igual a la tabla que se hace referencia dentro del parentesis que es Products en ProductID.
Ahora si cada fila tiene su propio nombre solamente.

    SELECT 	ProductID,
		Quantity, 
		(SELECT ProductName from Products  where OD.ProductID = ProductID) as Name
    FROM OrderDetails as OD

Tambien podemos renombrar la tabla a OD igual podemos omitir el "as".

    SELECT 	ProductID,
		Quantity, 
		(SELECT ProductName from Products  where OD.ProductID = ProductID) as Name,
		(SELECT Price from Products  where OD.ProductID = ProductID) as Price
    FROM OrderDetails as OD

Ahora tambien hemos traido el precio.

    SELECT ProductID, SUM(Quantity) as total_vendido,
		(SELECT price from Products where ProductID = OD.ProductID) as Price,
		(SELECT ProductName from Products where ProductID = OD.ProductID) as Name,
		(sum(Quantity)*(SELECT price from Products where ProductID = OD.ProductID)) as total_recaudado
	from OrderDetails OD
    group by ProductID
    ORDER By total_recaudado DESC

SI requiero que no se vea una columna en especifico podemos usar una subconsulta

    SELECT ProductID, SUM(Quantity) as total_vendido,
		(SELECT ProductName from Products where ProductID = OD.ProductID) as Name,
		(sum(Quantity)*(SELECT price from Products where ProductID = OD.ProductID)) as total_recaudado
	from OrderDetails OD
	where (SELECT price from Products where ProductID = OD.ProductID) > 40
    group by ProductID
    ORDER By total_recaudado DESC

Podemos acceder desde el from a esta nueva tabla.

    SELECT 	* FROM  (SELECT ProductID, SUM(Quantity) as total_vendido,
		(SELECT ProductName from Products where ProductID = OD.ProductID) as Name,
		(sum(Quantity)*(SELECT price from Products where ProductID = OD.ProductID)) as total_recaudado
	from OrderDetails OD
	where (SELECT price from Products where ProductID = OD.ProductID) > 40
    group by ProductID
    ORDER By total_recaudado DESC)

### 5. Ejercicio de subconsultas

***1.- Cantidad de ventas de un empleado.***

    SELECT FirstName, LastName,
	(SELECT SUM(od.Quantity) FROM Orders o, OrderDetails od
	WHERE o.EmployeeID = e.EmployeeID and od.OrderID = o.OrderID) as unidades_totales
    FROM Employees e
    where unidades_totales < (SELECT avg(unidades_totales) FROM (

    SELECT (SELECT SUM(od.Quantity) FROM Orders o, OrderDetails od
    WHERE o.EmployeeID = e2.EmployeeID and od.OrderID = o.OrderID) as unidades_totales from Employees e2
    GROUP BY e2.EmployeeID
    ))

Estamos seleccionando el Nombre y los apellidos de los empleados, ademas seleccionamos el promedio de unidades totales.
Seleccionado de empleados.

Filtrado por el promedio de los úmeros totales.

### 6. Joins 

Combina dos tablas y nos devuelve una nueva tabla.

Los mas comunes son:

1.- Inner join
2.- Left join
3.- right join
4.- full join
5.- cross join

**Forma implicita**
#### Cross join
implicito

    SELECT * from Employees e, Orders o

combina lasa dos tablas
Explicito

    SELECT * from Employees e cross JOIN Orders o

El cross joing nos regresa una nueva tabla con todas las combinaciones de filas que pueda existir, si tenemos una tabla de 5 filas y otra de 2, las posibles combinaciones serian 10.

#### Inner join
Inner join implicito

    SELECT * from Employees e, Orders o
    WHERE e.EmployeeID = o.EmployeeID

De esta manera combinamos solo los que tengan EMployeeID similar, este es un Inner join Explicito

    SELECT * from Employees e
    INNER JOIN Orders o ON e.   EmployeeID = o.EmployeeID

#### Crear una nueva tabla llamada Rewards

    CREATE TABLE "REWARDS" (
    "RewardID" INTEGER,
    "EmployeeID" INTEGER,
    "Reward" INTEGER,
    "Month" TEXT,
    PRIMARY KEY("RewardID" AUTOINCREMENT)
    )

Creamos la ID tipo entero, Empleado tipo entero, Recompensa que será dinero tipo entero, mes tipo texto, y convertimos RewardID a una clave primaria.

Insertamos Valores

    INSERT INTO REWARDS (EmployeeID,REWARD,Month) VALUES
    (3,200,"January"),
    (2,180,"February"),
    (5,250,"March"),
    (1,280,"April"),
    (8,160,"May"),
    (null,null,"June")

Aplicamos el **INNER JOIN**

    SELECT FirstName, LastName,Reward,Month FROM Employees e
    INNER JOIN REWARDS r ON e.EmployeeID = r.EmployeeID

Nos arroja solo los valores de nombre, apeido, recompensa y mes correspondiente.

**LEFT JOIN**

    SELECT FirstName, LastName,Reward,Month FROM Employees e
    LEFT JOIN REWARDS r ON e.EmployeeID = r.EmployeeID

Con **left join** me arroja todos los valores de la tabla de A y parte de la tabla B, en caso de que no exita valor, nos arroja **Null**

**RIGHT JOIN**

Lamentablemente SQlite no soporta el Right join por lo que podemos simular un right join invirtiendo las tablas

    -- Simulando un RIGHT JOIN invirtiendo las tablas REWARD y EMPLOYES
    SELECT FirstName, LastName,Reward,Month FROM REWARDS r 
    LEFT JOIN Employees e ON e.EmployeeID = r.EmployeeID

Agregamos un comentaria para que se entienda la operación, en otras bases de datos si funciona y solo podemos cambiar el left por el right

### 7. UNION y UNION ALL


**FULL JOIN**

En SQLite tampoco soporta el FULL JOIN por lo que simularemos el con **UNION**.

El cual nos permite unir dos consultas direferentes

    --Simulando un Full join uniendo un left join con una simulación de right join--
    SELECT FirstName, LastName,Reward,Month FROM Employees e
    LEFT JOIN REWARDS r ON e.EmployeeID = r.EmployeeID

    UNION
    
    -- Simulando un RIGHT JOIN invirtiendo las tablas REWARD y EMPLOYES
    SELECT FirstName, LastName,Reward,Month FROM REWARDS r
    LEFT JOIN  Employees e ON e.EmployeeID = r.EmployeeID

Unión nos permite recibir los campos sin que se Repitan. 
**UNION AL** nos arroja todos los valores incluso los repetidos.

***Cuando unas Columnas con union es necesario que tengas las mismas cantidades de columnas porque puede causar errores***


### 8. Cardinalidad 

La Cardinalidad en el contexto de base de datos se usa para especificar la relación entre dos entidades(Tabla).
 Cardinalidades

 **1:1** Uno a uno
Un registro de una tabla se relaciona con solo un registro de otra table

**1:N** Uno a Muchos
Un registro de la tabla se puede relacionar con diferentes registros de otra tabla.

**N:1** Muchos a uno
Muchos registros se relacionan con solo un registro de otra tabla

**N:M** Muchos a Muchos
Diferentes registros puede que se relaciones con muchos registro de otra tabla. Por lo que mantener este tipo de tablas es muy complicado por lo que se crean tablas intermedias que nos permitan gestionar la información.
**Notación de Martin**
![Notación de Martin](./../img/Captura%20de%20pantalla%20(167).png)


**Diagrama con notación de Martin**

![Diagrama de Martin](./../img/Captura%20de%20pantalla%20(168).png)


### 9. Normalización

Es un proceso dentro de las bases de datos para eliminar anomalias en los datos, hacer la base de datos mas eficiente

Tenemos 5 niveles de Normalización
Niveles **FORMA NORMAL**

1.- (1NF) Fist Normal Form
Consiste en garantizar cada atributo en una tabla tenga un valor único atómico, significa que los valores en una tabla no tienen que ser conjuntos, listas, o cualquier estructura de datos compleja.

Ningún dato de la columna no se repita y que los valores esten distribuidos en las columnas.

2.- (2NF) Second Normal Form
Establece que cada atributo que no sea una clave, dependa de la Clave primaria al 100 %, Si no se tiene que crear una tabla aparte.

3.- (3NF) Third Normal Form
Establece que cada atributo debe depender de la clave primario y no de otros atributos que no sean claves. Eliminamos la dependenciatransitiva

**En la vida cotidiana normalizar hasta la forma normal 3 es suficiente**

4.- (4NF) Fourth Normal Form
Se refiere a una forma en la que intentamos eliminar la redundancia de datos y las anomalias de actualización.

5.- (5NF) Five Normal Form
Se utiliza para bases de datos muy grandes.
Se asegura que no existan dependencias de union entre los atributos.

¿Como se aplican?

Primero se identifican las claves primarias.
Segundo dependencias funcionales

### 10. Índices 
**Indices primarios**
Como las Primary Key

**Indices Ordinarios**
Puede tener valores nulos y repetidos
Por ejemplo si tenemos la siguiente busqueda en la base de datos

    SELECT * FROM Products WHERE ProductName = "Chais"  

Tiempo de ejecucion 5ms

Pero necesitamos realizarla frecuentemente, podemos indexarla al Indice

     CREATE index name ON Products(ProductName)

De esta manera disminuimos su tiempo de ejecución.

**Indices Unicos**
     CREATE UNIQUE index name ON Products(ProductName)

Si agregamos un **UNIQUE** nos permite el bloquear que se registren datos repetidos como si fuera un primary key.

**Indices Compuestos**
     CREATE UNIQUE index names ON Employees(FirstName,LastName)

Incluso podemos ponerlo compuesto de manera que no se repitan valores identicos den combinación.

**Desventajas**
Los indices consumen mucho espacio en disco e incluso atrasar el rendimiento.
Mientras más indices mas complejo mantenerla, solo seleccionar índices que sean funcionales

Se recomienda utilizar en donde usemos constantemente valores que nos permitan eficientar tiempos.
Cuando se Tiene una alta cardinalidad, Si tenemos muchos datos que deben de ser datos únicos.

### 11. Vistas 

Las vistas son tablas virtuales.

    SELECT ProductID, ProductName,Price FROM Products
    WHERE ProductID > 20
    ORDER BY ProductID DESC

Si queremos obtener los valores ProductId, ProductName, Price usamos la misma consulta que ta hemos practicado antes.

    CREATE VIEW Prodctos_simplificados AS

    SELECT ProductID, ProductName,Price FROM Products
    WHERE ProductID > 20
    ORDER BY ProductID DESC

Listo podemos acceder a esta nueva tabla virtual llamada Productos_simplificados

    SELECT * FROM Productos_simplificados

Pdemos hacerlos mas veces? En terminos de rendimiento no es recomendable usarlo muchas veces.
De igual manera, tener cuidado con los nombres para evitar tener tablas con el mismo nombre.

Debido a que se le da prioridad a la tabla virtual

    DROP VIEW Productos_simplificados

Asi eliminamos la vista

    DROP VIEW if EXIST Productos_simplificados

Con esto nos evitamos obtener errores si la tabla ya no existe.

