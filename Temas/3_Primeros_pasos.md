### Primeros Pasos Código

Crear nueva base de datos
**1: CREATE DATABASE "Nombre de Base de datos"**

    Tabla:estructura de datos en filas y en columnas(Table)

Almacenan Campos que son los titulos de las columnas(Field)
El registro es una Fila(record)

Nuestro dato puede ser de tipo

    Int: entero
    Text: texto
    BLOB: Binario(Archivos imagenes)
    Real: Float(8 bytes) y rapido
    Numeric: Numeros enormes cualquier tamaño y mayor precision y lento

SQLite es uno de los pocos gestores que acepta cualquier tipo de dato de entrada, es un gestor dinamicos ya que convierte la casilla en el tipo de dato que le introduzcamos

    Sin embargo esto es una mala práctica, no es recomendable hacerlo.


    CREATE TABLE "users" (
	"nombre"	TEXT,
	"Apellido"	TEXT,
	"Edad"	INTEGER
    );

Para realizar consultas usamos

**2: SELECT * FROM users**

    Select: Queremos realizar una consulta
    *: Selector todo    
    From: de que tabla
    users: tabla

**3: INSERT INTO users (name, lastname,age)
VALUES ('Moises','Mendoza','25')**

    Insert into users: introducir dato en tabla
    Values: valores

**4: INSERT INTO users (name,lastname,age)
VALUES ('Aaron', 'Mendoza', 22),
		('Alejandra','none',17)**

Con la consulta select podemos acceder a una tabla ya creada o crear una nueva tabla

**5: SELECT name,age FROM users**

    Así visualizamos la nueva tablo con solo dos valores

|name|age|lastname|
|---|---|---|
|Moises|Mendoza|25|
|Aaron| Mendoza|22|
|Alejandra|none|17|

----------