## CONCEPTOS BÁSICOS DE SQL

### ¿Que es SQL?
Structure Query language
Lenguaje de consultas estructuradas.

Es un lenguage estandarizado, es decir que una vez que lo aprendas podrás utilizarlo dentro de otras herramientas ya que usan la misma estructura sin tener que reaprender uno nuevo.

### Historia y usos

Anteriormente usabamos lista de información separadas por signos quenos permitian almacenar la información de mejor manera, sin embargo acceder a ella era muy complicado.
Permitia usa la información de manera 

    Ordenada
    Sencilla
    Sin mayores inconvenientes

Por otro lado tenemos a "Edgar Cold" que inventó el Algebra relacional, que sirve para crear conjuntos y trabajarlos.
Entonces penso en crear una base de datos basada en el algebra relacional.

De ahí nacio SQL que es basicamente algebra relacional.

Con SQL podemos crear y administrar bases de datos.
Permite realizar consultas, modificar, eliminar, poner restricciones para asegurar los datos, permitiendonos tener datos precisos y consistentes.

### Diagrama ER (CHEN)

#### Entidad
¿Que es una entidad? Es como un objeto, puede hacer referencia a un cualquier cosa o concepto, es una representación de algo.

Por ejemplo en un tienda en linea las entidades pueden ser los clientes, productos, ordenes de compra y proveedores.

y la nomenclatura usada para representar las entidades se llama notacion de CHEN.

    Las identidades comunmente se representan encerrandolas en un cuadrado.

Que es lo que hace que una identidad sea una identidad: sus atributos

    Los atributos los representamos con un ovalo.

Existen los atributos Simples y los Compuestos.

Los simples tienen datos unicos.
Y los compuestos ademas se componen de otros atributos 
    
    Se representan enlazandolos con lineas

Atributos Multivalor, son los que contienen más de un valor

    Se repesentan por estar encerrado entre dos ovalos.

Atributos derivados podemos obtenerlos a partir de otros atributos.

    Los identificamos con un borde punteado

#### Key
Una Key es un atributo único que lo diferencia de otro parecido para volcerse único

    Lo representamos subrayandolo

#### Ejercicio 1

Pensar una entidad que tenga 5 atributos

    1 Multivalor
    1 key
    3 aleatorios

    Persona:
    atributo multivalor: Hobies
    Atributo Key:       CURP
    Atributo derivado: Fecha de cumpleaños, edad
    Atributo simple:    Nombre
    Atributo simple: Fecha de Nacimiento 

No es necesario tener un dato como Fecha separadopor día,Mes y Año. Es mejor mantenerlo todo Conciso, Preciso y No redundante.