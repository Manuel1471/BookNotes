# Elixir Book (Elixir 1.7)

## Resumen del libro

Este libro ayuda a adentrarse al mundo de elixir.

## Introduccion

Elixir nacio de ser la solucion de un problema con BEAM (Maquina virtual de Erlang).

Erlang permite desarrollar estructuras complejas clientes-servidor con un alto grado de concurrencia, tolerancia a fallos y alta disponibilidad entre otras cosas de forma facil y sencilla.

A diferencia de Erlang, Elixir tiene una gran versatilidad y facilidad para escribir codigo cada vez mas compacto y con una mayor potencia. Lo que puedas hacer con Erlang lo puedes hacer con Elixir.

## Chapter 1 "Lo que debes saber de elixir"

La necesidad de soluciones de alta capacidad para soportar una inmensa cantidad de peticiones a un sistema dio a lugar el uso de soluciones con Erlang o Elixir.

Elixir es un lenguaje de programacion funcional con capacidad de meta-programacion, la mayoria de Elixir fue creado en Elixir gracias a su metaprogramacion.

Elixir tiene mucha azucar sintetico. (Azucar sintetico son construcciones que no aportan nuevas funcionalidades pero ayudan a la facilidad de escribir codigo)

Todo Elixir gira alrededor de las funciones, macros y el flujo de datos.

En otros lenguajes las estructuras condicionales como if pertenecen al propio lenguaje, en Elixir esta definida a traves del propio lenguaje.

Elixir solo tiene 8 palabras claves.

Al igual que Erlang en Elixir podemos usar los procesos de BEAM, esto dota de las siguientes ventajas al lenguaje:

    - Desarrollo de soluciones de alta concurrencia.
    - Al capacidad para recibir peticiones al mismo tiempo
    - Tolerancia a fallos
    - Emplear codigo de Erlang

Como podemos leer, necesitamos separar las caracteristicas que tiene la maquina virtual BEAM de lo que hace Elixir, ya que las caracteristicas de BEAM las tienen todos los lenguajes que compilan y corren las aplicaciones.

### BEAM

Es una maquina virtual creada y mantenida por multiples empresas desde hace muchos años.

Nacio para dar soporte a sistemas de telecomunicacion con unas caracteristicas basadas en la tolerancia a fallos, alto nivel de concurrencia, alta capacidad, tiempo real blando y actualizacion en caliente para evitar apagar el sistema.

- Tolerancia a fallos: Se aisla el codigo en unidades minimas de ejecucion llamadas procesos. Un proceso es iniciado y debido a un fallo puede ser termindo. Al mantener aislados los procesos y sin memoria compartida garantiza la no falla de otros procesos del sistema. De esta forma el sistema sigue sin el proceso que fallo.

- Alto nivel de concurrencia: Al no existir memoria compartida los recursos no son compartidos en ningun momento. Entonces la parte llamada "Modelo de proteccion de seccion critica" se basa en mantener la unidad de ejecucion conjunta con datos que maneja y ningun otro codigo puede acceder a esa informacion. Eso garantiza un control de acceso a informacion compartida y evita situaciones de volatilidad.

- Alta capacidad: BEAM define unos procesos internos muchos mas ligeros que los que da el sistema operativo. Esto permite generar muchos procesos mas que el sistema operativo.

        Sistema operativo: 65,536 procesos (16bits)
        BEAM: 134,000,000+ procesos

    Esto permite la capacidad de atender miles y millones de peticiones con un gasto computacional menor.

- Tiempo real blando: Al no existir la memoria compartida, el recolector de basura de BEAM no necesita bloquear ningun proceso para actuar. Esto se traduce en eliminacion de cortes en el funcionamiento de la VM y poder trabajar en tiempo real blando.

- Actualizacion en Caliente (Hot Reload): BEAM es una de las unicas maquinas virtuales que dispone de un sistema seguro para el cambio de codigo en caliente. Permite modificar el codigo de un modulo aun manteniendo una copia antigua de los procesos en ejecucion e ir migrando la nueva version del modulo de forma segura.

### Elixir

Elixir es una potencia en la meta-programacion que nos ayuda a reducir la repeticion una y otra vez de los mismos codigos y reduce al minimo las plantillas de codigo a completar cuando se usan frameworks.

Parte del codigo se ejecuta en tiempo de compilacion con el objetivo de mejorar otro codigo mas completo o preciso y asi mejorar el rendimiento en tiempo de ejecucion.

- Lenguaje Dinamico: Es de tipado Dinamico y no es fuertemente tipado. Los tipos son opcionales y con fines de comprobacion y documentacion.

- Productividad: Al permitir generar codigo con codigo permite eliminar la necesidad de escribir mucha repetitividad y agregar construcciones especificas en logica de negocio facilitando y reduciendo la generacion de codigo.

- Extensibilidad: A traves de la definicion de macros, guardas, funciones, sigilos y sobretodo protocolos nos permite agregar muchas mas construcciones al lenguaje. La extensibilidad tiene como piedra angular el polimorfismo y las estructuras.

- Concurrencia: Dada por BEAM. A traves de comportamientos definidos desde la base a traves de OTP el lenguaje construye elementos permitiendo mantener la base de paso de mensajes, mantener la seccion critica y facilitar la creacion de miles o millones de procesos.

- Interoperatividad: Es posible sin mucho problema agregar codigo desde Erlang y emplearlo en Elixir de forma facil.

-Evaluacion perezosa y/o creacion de generadores: Elixir nos da la posibilidad de evaluar los elementos uno a uno en la cadena de proceso del algoritmo ahorrando asi memoria y tiempo del procesador.

### Historia de BEAM

La idea de Erlango surgio por la necesidad de Ericsson de acotar un problema que habia surgido en su plataforma AXE, que estaba siendo desarrollada en PLEX, un lenguaje propietario.

Amstrong, Elshiewy y Robert Virding desarrollaron una logica concurrente de programacion para canales de comunicacion.

Este algebra de la telefonia permitia a traves de su notacion describir el sistema publico de telefonia (POTS) en tan solo quince reglas.

Al llevar esta teoria a la practica desarrollaron modelos en Ada, CLU, SmallTalk y Prolog entre otros. Esto descubrio que la teoria se procesaba de forma rapida en lenguajes de alto nivel.

La conclusion que se llego fue que si se puede resolver matematicamente y portar ese esquema a un programa de forma que el esquema funcional se respete y entienda tal y como como se formulo fuera del enterno computacional, puede ser facil de entender, mejorar y adaptar el esquema.

El siguiente problema que se toparon es que prolog no era un lenguaje de concurrencia aunque si de alto nivel, decidieron realizar uno que satisfajera todos sus requisitos, basandose en las ventajas de prolog.

Erlang vio a luz en 1986, los requisitos que se buscaron cumplir fueron:

- Los procesos debian ser una parte intrinseca del lenguaje, no una libreria o framework de desarrollo.
- Debian por ejecutarse desde miles a millones de procesos concurrentes y cada proceso independiente del resto, de modo que si alguno se corrompiera no fallara todo el sistema.
- Debe poder ejecutarse de manera ininterrumpida, lo que obliga a no detener su ejecucion para actualizar el codigo del sistema.

Despues de que Erlang saliera a la luz, llegaron los problemas, el primero en 1989, este problema era al respecto de que su rendimiento no era adecuado. La necesidad a cumplir eran al menos 40 veces mas rapido como minimo.

Mike Williams se encarga de escribir el emulador, cargador y recolector de basura (en lenguaje C) mientras Joe Armstrong escribia el compilador, las estructuras de datos, el heap de memoria y la pila; por su parte Robert Virding se encargaba de escribir librerias.

Llego hasta el punto en que Erlang se optimizo a un punto de ser 120 veces mas rapido de lo que era el interprete de Prolog.

En los 90's, tras desarrollar productos de AXE con este lenguaje, se le potencio agregando elementos como:

- Distribucion
- Estructura OTP
- HiPE (Grupo de investigacion que paso codigo a lenguaje maquina)
- Sintaxis de bit
- Compilacion de patrones de matching.

Al final en esa epoca, tenia algunos problemas para ser adoptado de forma amplia ademas de que fue el periodo de Java.

Despues de un tiempo la comunidad fue creciendo fuera de Ericcson, el equipo OTP siguio desarrollando y soportando Erlang con las siguientes acciones:

- Continuo el proyecto HiPE
- Seguimiento en aplicacion EDoc
- Seguimiento en aplicacion Dialyzer

En los años mas actuales se han agregado las siguientes caracteristicas a Erlang:

- La capacidad de SMP
- La capacidad multi-core

Actualmente el rendimiento es al menos 300 veces mas rapido que la version del emulador escrita en C, por lo que es 36,000 veces superior a la version en prolog.

### El comienzo de Elixir

Jose Valim ha sido uno de los mayores contribuidores mas activos a Rails y ante los problemas existentes para poder hacer funcionar Rails con websockets o la seguridad entre hilos al ejecutar Rails en un entorno con multiples nucleos se decidio a probar nuevas vias.

Al principio la idea de Elixir fue construir un Ruby sobre BEAM. Tal como intento REIA. Jose Valim se baso en Reia para iniciar Elixir y cuando Elixir comenzo a incrementar la velocidad de su desarrollo fue cuando el desarrollador de Reia considero abandonar el proyecto y dar su apoyo a Elixir.

### Desarrollos con Elixir

A nivel empresarial Elixir es usado por empresas tan grandes como Adobe, AdRoll, Lexmark, PagerDuty, Pinterest o Slack.

Dado su origen el principal uso de Elixir esta en la elaboracion de servicios web y websocket para servicios en internet. Uno de los grandes frameworks que posibilita y facilita esta adopcion es Phoenix Framework.

## Chapter 2 El lenguaje

La sintaxis de Elixir esta basada en otros lenguajes como Ruby y Erlang y agrega el suficiente azucar sintactico para dar flexibilidad al programador para escribir codigo simple. Permite expresar facilmente el codigo escrito. No obstante debemos recordar que Elixir es un lenguaje funcional.

### El interprete de Elixir (iex)

La mayoria del codigo de ejemplo se ejecuta en la linea de comandos o el interprete de Elixir llamada iex.

Al acceder al interprete deberias ver una linea de codigo asi:

$ iex
Erlang/OTP 21 [erts-10.1.3] [source] [64-bit] [smp:8:8]
[ds:8:8:10] [async-threads:1] [hipe] [kernel-poll:false]
[dtrace]
Interactive Elixir (1.7.4) - press Ctrl+C to exit (type h()
ENTER for help)
iex(1)>

Este te explica lo siguiente:

La primera linea es informacion sobre BEAM indicando la version de Erlang/OTP. Indica la instalacion desde codigo fuent(source) ejecutandose en un sistema de 64 bits, con uso de SMP (Indica varias unidades de procesamiento que acceden a la misma memoria) seguido por la configuracion del programador de tareas,los hilos asincronos lanzados, el uso de HiPE, poll del kernel (tecnicca de E/S para delegar la espera por entrada de datos al nucleo del sistema operativo y liberar el programador de tareas) y dtrace (Herramienta que permite obtener eventos del sistema operativo sobre el uso de recursos como la red, disco, memoria y mas).

### Comentarios

Los comentarios son esa parte del codigo no ejecutable que sirve al programador para aclarar una parte del codigo. Elixir agrega comentarios empleando el simbolo almohadilla (#)

```elixir

# Este código calcula el área del rectángulo:
area = base * altura # multiplica área por base

```

### Tipos de datos

En Elixir disponemos de distintos tipos de datos desde los mas simples como:

- atomos
- numeros

Hasta estructuras compuestas por otros tipos de datos como:

- mapas
- listas

Cada tipo de dato tiene sus propias particularidades y su cometido.

Se responderan tres preguntas basicas:

- ¿Que son?
- ¿Para que se usan?
- ¿Como se usan?

Cada tipo de dato ademas tiene asociado un modulo que permite realizar acciones sobre el mismo o conversiones desde otros tipos de datos, estos modulos se dejan a lectura del lector de estas notas.

#### Atomos

Los atomos son una unidad muy pequeña y autoexplicativa que podemos usar para agregar codigo mas legible y errores mas comprensibles en consola al emplear texto en lugar de numeros para indicar estados, codigos de error, o indicadores para configuracion entre otros.

Este tipo de dato nos ayuda a dar nombre al contenido de variables sin necesidad de ocupar mucho tamaño de memoria.

Ejemplo:

Problema
Indicar el estado de una cuenta de restaurante en todo momento.

##### Solucion 1

Crear un valor numero para indicar estados como

- 0 es "nuevo"
- 1 es "en proceso"
- 2 es "cancelado"
- 3 es "pagado"

**Nota**: Esto aumenta la dificultad de la lectura del codigo ademas del trabajo de crearlas y mantenerlas

##### Solucion 2

Emplear texto para indicar el estado como

- "nuevo"
- "en proceso"
- "cancelado"
- "pagado"

**Nota**: Obtienes un codigo legible pero con mayor uso de memoria y mas lento de procesar si un texto es igual a otro

Para solventar este problema surgieron los atomos. Este tipo de dato se expresa con un texto comprensible para el lector. Donde al final puedes utilizar esta solucion:

##### Solucion Elixir

Emplear los atomos para indicar los estados de la cuenta.

- :nuevo
- :en_proceso
- :cancelado
- :pagado

**Nota**: Como se ve mas adelante este tipo de dato es muy eficiente en memoria

El atomo es incluso mejor en comparacion con emplear numeros y el rendimiento mucho mayor a emplear cadenas de texto.

**Importante**: Cada atomo se inserte en una tabla definida por 1,048,576 lugares. Si inserta mas se produce un error critico y BEAM termina su ejecucion por completo.

Para evitar llenar la tabla de atomos, se tiene que evitar emplear atomos que se generen de forma dinamica y si es necesario hacer uso de la funcion String.to_exiting_atom/1 que checa que no este repetido el atomo para ser reutilizado.

#### Booleanos y logicos

Este tipo de dato tiene dos representacion posibles true o false. Se obtienen principalmente a traves del uso de los literales y los operadores de comparacion ademas de los nexos logicos.

**Dato interesante**: En si la representacion interna de este dato no existe. Son en realidad los atomos :true y :false.

#### Valor nulo nil

El valor nulo o nil es otro atomo con significado especial que permite escribirse sin el uso de los dos puntos. El significado del atomo es la ausencia de tipo. Cuando asignamos este valor a una variable estamos indicando que no dispone de tipo.

#### Numeros enteros y reales

En Elixir puedes trabajar con dos tipos de numeros:

- enteros: no tienen decimales
- reales: tienen decimales

**Nota**: Los numeros enteros no tienen un tamaño definido sino que el limite es la cantidad de memoria que tenga el sistema

Podemos especificar la base en la representamos los numeros enteros anteponiendo un prefijo especifico a cada numero escrito.

- Hexadecimal (0x)
- Binario (0b)
- Octal (0o)

Los numeros reales se representan en su formacientifica si exceden cierta dimension. Se puedes escribir de dos formas posibles:

- 20.0
- 2.0e1

#### Variables e Inmutabilidad

Las variables son nombres a los que se asigna un valor. Podemos emplear un nombre que este compuesto por letras, numeros y guion bajo o subrayado aunque con algunas excepciones.

Las variables refencian valores. Estos valores pueden ser literales, el dato en si pueden ser otras variables o expesiones que contengan llamadas a funciones y calculos aritmeticos o logicos.

A diferencia de otros lenguajes las variables de Elixir refencian espacios de memoria y cuando se asigna a otro valor referencian a ese nuevo espacio de memoria. La variable en ningun momento cambia el valor en el espacio de memoria que tenia asignado.

En elixir existe la inmutabilidad para los datos. Es decir, un tipo de dato como una lista, un mapa, una cadena de texto o incluso un numero no cambian. Su espacio de memoria no varia una vez se ha reservado para contenerlo. Si queremos modificar un dato se crea un espacio de memoria nuevo con la modificacion.

```elixir
    iex> a = 10
    10
    iex> b = a
    10
    iex> a = 5
    5
    iex> b
    10
```

El uso de memoria no suele ser un problema porque cada proceso tiene su espacio de memoria y cuando una funcion termina la reserva de memoria se desecha excepto el retorno de la funcion.

#### Listas

Las listas en Elixir son vectores de informacion heterogenea, es decir, pueden contener informacion de distintos tipos, ya sean numeros, atomos, tuplas, estructuras, mapas u otras listas.

Elixir maneja las listas como lenguaje de alto nivel, en modod declarativo, permitiendo el uso de herramientas como las listas de compresion o la agregacion y eliminacion de elementos especificos como si se tratase de un conjunto.

#### Las listas de caracteres

Son un tipo especifico de lista. Se trata de un lista homogenea de elementos representables como caracteres.

 **Importante**: Esta forma de tratar las cadenas es muy similar a la que se emplea en C, donde el char es un dato de 8 bits en el que podemos almacenar un valor de 0 a 255 y que las funciones lo tomaran como representancion de la tabla. En elixir, la unica diferencia es que cada dato no es de 8 bits sino un entero aunque consume mas memoria, da soporte a las tablas UTF-8 y UTF-16.

#### Colecciones

En general las listas son consideradas colecciones de datos en Elixir. Pero no solo las listas. Podemos encontrar otro tipo de datos que se concideran colecciones.

A estas colecciones se les puede aplicar un modulo llamada Enum, este modulo nos permite realizar acciones sobre las colecciones.

**Nota**: Se deja a considerar el leer las funciones del modulo. El requisito para usar este modulo es que se implemente el protocolo Enumerable.

#### Cadenas de texto

Las cadenas de texto o cadenas de caracteres son similares a las listas de caracteres. Permiten almacenar cadenas de caracteres con tamaño de byte y permite realizar trabajos especificos con secuencias de bytes o incluso nivel bit.

Las cadenas pueden ser representadas con caracteres o como una lista binarias.

```elixir
    iex> "Hola"
    "Hola"
    iex> <<72,111,?l,?a>>
    "Hola"
```

#### Trabajando con Binarios

Las cadenas de caracteres nos permiten trabajar con cadenas de texto como listas binarias.

Esta funcionalidad nos permite empaquetar en forma binaria un conjunto de informacion teniendo control incluso a nivel de bit a cada uno de sus componentes.

```elixir
iex> <<cabeza::binary-size(1), cola::binary>> = "Hola"
"Hola"
iex> cabeza
"H"
iex> cola
"ola"
```

Esta sintaxis es un poco mas elaborada que la de las listas, pero se debe a que nos adentramos en la verdadera potencia: el manejo de bits.

#### Trabajando con Bits

En la seccion pasada vimos la sintaxis para simular el comportamiento de la cadena al tomar la cabeza de una pila.

Esta es **var::tipo-tamaño(n)**

En caso de que no se indique el tamaño, se asume que es tanto como el tipo soporte.

como tipo podemos indicar varios elementos. Los tipos tienen una forma compleja pero siguen una sintaxis: **endian-signo-tipo-unidad**, esta es la explicacion para cada uno:

- endian: La forma en que los bits son leidos en la maquina. Estos son el formato intel o morotola, es decir, littel o big respectivamente, aunque tambien es posible elegir native, que empleara el formato nativo de la maquina.
```élixir

    iex> <<1215261793::big-size(32)>>
    "Hola"
    iex> <<1215261793::little-size(32)>>
    "aloH"
    iex> <<1215261793::native-size(32)>>
    "aloH"
```

- signo: Se indica si el numero se almacena en formato con signo o sin el, es decir, signed o unsigned, respectivamente.

- tipo: Es el tipo con el que se almacena el dato en memoria. Segun el tipo el tamaño es revelante para indicar la precision o numero de bits. Los tipos disponibles son:
  
  - integer
  - float
  - binary
  - bits(bitstring)
  - bytes(binary)
  - utf8
  - utf16
  - utf32

- unidad: Es el valor de la unidad por el que multiplicara el tamaño. En caso de enteros y coma flotante el valor por defecto es 1 y en caso de binario es 8. POr lo tanto: **Tamaño X Unidad = Numero de bits**.

#### Tuplas

Las tuplas son tipos de datos organizativos en Elixir. Se pueden crear listas de tuplas para conformar conjuntos de datos homogeneos de elementos individuales heterogeneos.

Las tuplas a comparacion de las listas, no pueden incrementar ni decrementar su tamaño salvo por la redefinicion completa de su estructura. Se emplean para agrupar datos con un proposito especifico.

Por ejemplo: Queremos almacenar esta información para poder tratarla y sabemos que va a ser: ruta, nombre, tamaño y fecha de creación.

``` elixir

    { "/home/user", "texto.txt", 120, {{2011, 11, 20}, {0, 0,0}} }
```

##### Modificacion dinamica de tuplas

