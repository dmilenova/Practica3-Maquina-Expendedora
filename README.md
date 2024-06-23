# Practica 3 Controlador Maquina Expendedora. Sistema empotrados y de tiempo real.
Introducción
En esta práctica, se nos ha solicitado diseñar, utilizando componentes y sensores básicos en Arduino, una máquina expendedora de café que pueda simular el servicio proporcionado a un cliente en la vida real. Además, incluye una interfaz de administración donde se pueden visualizar los datos de los diferentes sensores implementados en el sistema, así como la opción de cambiar los precios de los productos.

Explicación de Ejecución y Métodos Utilizados
Para llevar a cabo esta práctica, utilicé la función millis() de Arduino para controlar los tiempos de ejecución de cada acción requerida, así como un controlador y varios hilos para gestionar los LEDs y el botón. Utilicé la clase LedThread, proporcionada en las diapositivas del curso, para controlar el parpadeo de los LEDs.

Primero, se declaran todas las variables usadas en el programa (pines de cada sensor, variables asociadas a estados del programa y variables referentes a los tiempos en segundos y los tiempos que utilizan la función millis()).

Luego, creé tres métodos que incluyen gran parte de la funcionalidad del programa:

administration_menu(): Este método representa la funcionalidad del menú de administración, con cuatro opciones entre las que podemos elegir. A través del joystick, podemos ver los datos de cada opción: 0 -> temperatura y humedad, 1 -> distancia, 2 -> contador, 3 -> modificar precios.

button_action(): Este método maneja las acciones según el tiempo que se mantenga pulsado el botón. Si se pulsa entre 2 y 3 segundos, se reinicia la función de servicio, mostrando el mensaje "ESPERANDO CLIENTE". Si se pulsa 5 segundos o más, se accede a la función de administración, y si ya estamos dentro, volvemos a la función de servicio.

read_joystick_values(): Este método se utiliza para leer los valores del joystick en función del eje X, permitiendo navegar tanto por el menú de servicio como por el de administración.

A continuación, se encuentra la función setup(), donde se configuran todos los pines a utilizar, así como la pantalla LCD, los diferentes usos de cada hilo y controlador, etc.

Finalmente, el programa principal se basa en una máquina de estados según las acciones realizadas con el botón y el joystick. El programa tiene cinco estados:

START: El programa arranca mostrando el mensaje "CARGANDO..." en el LCD, mientras el LED1 parpadea 3 veces a intervalos de un segundo. Luego, pasa al estado 2.

WAITING_CUSTOMER: En este estado, el LCD muestra el mensaje "ESPERANDO CLIENTE" hasta que el sensor de ultrasonido detecta algo a menos de 1 metro, pasando al estado 3.

CUSTOMER_FOUND: Al detectar un cliente a menos de 1 metro, se muestran los datos de temperatura y humedad durante 5 segundos. Luego, se muestran los productos disponibles con sus precios. Una vez seleccionado un producto con el joystick, se pasa al siguiente estado.

PREPARING_COFFEE: Cuando se selecciona un producto, el LCD muestra "PREPARANDO CAFE..." durante un tiempo aleatorio entre 4 y 8 segundos, mientras la intensidad del LED2 aumenta proporcionalmente. Finalmente, muestra "RETIRE BEBIDA" durante 3 segundos y vuelve al estado de espera, mostrando "ESPERANDO CLIENTE".

ADMINISTRATOR: Para acceder a este estado, se debe pulsar el botón 5 segundos o más. Aquí se muestran varias opciones como ver los datos del sensor de temperatura, del sensor de distancia, un contador de segundos del programa y una opción para modificar los precios de cada producto. Para salir, se debe pulsar nuevamente el botón durante 5 segundos o más.
![Esquema](esquema_practica3.pdf)
