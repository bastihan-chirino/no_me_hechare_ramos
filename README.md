# no_me_quiero_hechar_ramos
1. El accidente de Mario
Mario sufrio un terrible accidente mientras tenia una de sus aventuras. Resulta que en su
camino cotidiano para ir a salvar a la princesa Peach, no logro levantar su pu~no para golpear un
bloque de concreto pegandole con la cabeza, sufriendo una contusion encefalo craneal dejandolo
en coma por varios meses. Al despertar, los doctores se llevaron la horrible sorpresa de que Mario
habia olvidado como ser el mismo. Su hermano Guiseppe, al recibir la noticia, se puso muy triste
y penso en hacer un programa en C que lo ayudara a recuperar la memoria, pero como esta
demasiado ocupado contando sus millones gracias a su exitosisimo lenguaje de programacion
Yahoo, te delego la tarea a ti.

2. Escenario
En el mundo existen cinco tipos de elementos, con sus respectivas caractersticas:

1. Personaje:
string: nombre
int: estado, 1: normal, 2: brillante, 3: mareado, 4: wario
int: cantidad de monedas

2. Objeto:
string: nombre
int: estado que otorga, 1: health, 2: mareado, 3: wario

3. Enemigo:
string: nombre

4. Bloque:
void: contenido del bloque
int: tipo que almacena, 0: monedas (int) o 1: Objeto

5. Suelo:
int: 0: piso firme o 1: agujero infinito

Existiria una lista enlazada donde cada nodo podra almacenera alguno de estos cinco elementos,
siguiendo la siguiente estructura:

typedef struct escenario {
casilla* curr;
casilla* head;
casilla* tail;
int length ;
int posCurr ;
} escenario;

typedef struct elemento {
void * caracteristica1;
void * caracteristica2;
void * caracteristica3;
} elemento ;

typedef struct casilla {
elemento cosa ;
int tipo;
casilla * next ;
} casilla ;
Se puede ver como cada casilla del escenario tiene un int para determinar que cosa hay
en esa casilla, estos corresponden a los indicados anteriormente. Ahora, cada elemento es una
estructura que consiste de 3 caractersticas maximo, puede tener menos.
Ademas, el escenario implementara las siguientes funciones:

1. MOSTRAR
Muestra el contenido de la casilla i, se tiene que mostrar de la siguiente forma:
Tipo
Nombre Caracteristica 1 : valor
Nombre Caracteristica 2 : valor
Nombre Caracteristica 3 : valor
Ejemplo, si quiero mostrar una casilla que contiene un Personaje llamado Baby Mario que
esta en estado mareado y con 0 monedas.
Personaje
nombre : Baby Mario
estado : Mareado
Cantidad de monedas : 0

2. MOSTRAR TODO
Mostrar el contenido de cada casilla como se muestra en la funcion mostrar yendo de la
posicion 0 hasta el final.

3. ANADIR ELEMENTO
A~nade un elemento en la posicion i.

4. BORRAR ELEMENTO
Borra un elemento en la posicion i.

5. BORRAR TODO
Borra todo el escenario (no mario no D:)

3. Acciones
El personaje tendra una serie de acciones a su disposicion, las cuales son:

1. SALTAR ENCIMA
Saltar encima recibira el escenario y un entero, el entero señalara cuanto espacio debe
saltar en relacion a la posicion actual del personaje (Ej: -1 salta uno hacia atras, 2 salta
dos hacia adelante)

2. CAMINAR EN
Caminar en recibira el escenario y debera mover el personaje a la siguiente casilla disponible.

3. TACLEAR AL FRENTE
Taclear al frente recibiria el escenario y debera mover el personaje una casilla hacia la
derecha.

4. RUSHEAR
Rushear recibiria el escenario y moveria al personaje tres casillas a la derecha.

5. VER PLATA
Ver plata muestra la cantidad de monedas que lleva recolectada el personaje por el momento.

Cada accion correspondera a una funcion. Las acciones no siempre se podran realizar, ya
que dependeran del estado del personaje. Para saber que acciones estan disponibles, existiria una
lista con puntero a funciones que contendran todas las acciones que el personaje puede realizar
con su estado actual (esto implica que las funciones que no puede realizar no deberian estar en
la lista). Para eso, se propone la siguiente estructura de trabajo:

typedef struct acciones{
  dun* curr ;
  dun* head ;
  dun* tail ;
  int l ength ;
  int posCurr ;
}  acciones;

typedef struct dun{
void * funcion;
int identificador;
} dun;

De esta forma, existira una lista con el puntero Void que apuntara a la funcion y un identi-
cador que indicara que funcion es.

3
4. Toda accion tiene una consecuencia
Cada accion a realizar tiene sus consecuencias y requisitos, a continuacion se listaran todos
estos casos:
Si el personaje salta encima de un enemigo, elimina al enemigo y toma su posicion.
Si salta encima de un objeto, toma su posicion eliminando el objeto y ganando el estado
que otorga.
Si salta encima de un bloque, elimina el bloque y obtiene las monedas/objeto.
Si taclea un enemigo, lo mata y toma su posicion.
Si taclea y no hay un enemigo, se queda en su misma posicion y entra en el estado mareado,
perdiendo la capacidad de saltar.
Rushear solo se puede utilizar si el personaje esta en estado brillante, despues de usarlo
pierde el estado.
Si Rushea, mata a todo enemigo que encuentre entre su posicion actual y la posicion final.
Cualquier movimiento que se tope con un agujero, mata al personaje y lo devuelve al
inicio.
Si camina y se encuentra con un enemigo, el personaje muere y vuelve al inicio.
Si esta en estado wario y rompe un bloque con monedas, recibe el doble de monedas y
pierde el estado
Si el personaje muere, regresa al estado normal.
El estado normal es el estado por defecto.
Siempre se a~nade el personaje en la casilla inicial.
Si el personaje toma un objeto con el estado health, el personaje vuelve al estado normal.
5. Funcionamiento
El programa debera primero permitir crear el nivel a traves de un menu por consola. Este
menu pedira primero el tama~no del nivel (todas las casillas se inicializaran como piso normal) y
nos permitira usar las funciones del escenario. Una vez terminemos de crear el escenario, debera
haber una opcion que nos permita pasar a la siguiente etapa. Se asume que siempre la primera
casilla contendra al personaje al inicio del juego.
En la siguiente etapa existira un menu donde podremos nombrar a nuestro personaje, utilizar
las funciones de escenario mostrar, mostrar todo y las acciones disponibles del personaje. Al
momento de ingresar una accion se debe utilizar una funcion llamada choice, que recibira la
lista de acciones disponibles y la accion pedida.
4
6. Definicion de funciones a realizar
void mos t rar ( e s c e n a r i o * esc , i n t i )
void mos t rar todo ( e s c e n a r i o * e s c )
void anadi r e l emento ( e s c e n a r i o * esc , elemento * e l e , i n t i )
void bo r r a r e l ement o ( e s c e n a r i o * esc , elemento * e l e , i n t i )
void bo r r a r t odo ( e s c e n a r i o * e s c )
void s a l t a r enc ima ( e s c e n a r i o * esc , i n t i )
void caminar en ( e s c e n a r i o * e s c )
void rushear ( e s c e n a r i o * e s c )
void v e r p l a t a ( e s c e n a r i o * e s c )
void cho i c e ( i n t accion , a c c i one s * l i s t aAc c , e s c e n a r i o * e s c )
7. Datos de Vital Importancia
Pueden crear todas las funciones que quieran, pero deben implementar las funciones de-
nidas y los struct.
Pueden crear archivos nuevos si los necesitan.
Consultas vía la plataforma oficial #AULA
Si la accion que se desea realizar no esta en la lista de acciones disponibles, imprima "OH
OH!", si la accion se puede realizar, se debe mostar "HICE nombre accion"
Si el personaje quiere avanzar al estar en el nal de la lista, se termina todo y debe aparecer
"Gracias alumnos de lp por ayudarme a recuperar la memoria, pero tu 100 esta en otra
tarea".
8. Archivos a Entregar
Resumiendo lo anterior, los archivos minimos a entregar son:
README.txt
escenario.c
escenario.h
acciones.c
acciones.h
main.c
MAKEFILE
El archivo escenario.c debe contener las funciones implementadas relacionadas al escenario.
El archivo acciones.c debe contener las funciones relacionadas a las acciones del personaje.
5
9. Sobre Entrega
El codigo debe venir indentado y ordenado.
Las funciones deberan ir comentadas, explicando clara y brevemente lo que realiza, los
parametros que recibe y los que devuelve (en caso de que devuelva algo).
Debe estar presente el archivo MAKEFILE para que se efectue la revision, este debe
compilar TODOS los archivos.
Se debe trabajar de forma individual.
La entrega debe realizarse en tar.gz y debe llevar el nombre:
Tarea2LP RolIntegrante.tar.gz
El archivo README.txt debe contener nombre y rol del alumno e instruccio-
nes detalladas para la compilacion y utilizacion de su programa.
La entrega sera va aula y el plazo maximo de entrega es hasta el 11 de Mayo a las
23:55 hora aula.
Las copias seran evaluadas con nota 0 y se informaran a las respectivas autoridades.
Si el make le no esta bien realizado, la tarea no se revisara.
