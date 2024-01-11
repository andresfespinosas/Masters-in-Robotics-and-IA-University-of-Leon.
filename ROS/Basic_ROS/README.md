Ejercicios
1. Crear un entorno de trabajo

Para crear un espacio de caktin workspace, se establece mediante el comando mkdir.

>mkdir -p ~/catkin_ws/src

Luego se ingresa a la carpeta donde se creo el nuevo entorno cone l comando cd.

>cd ~/catkin_ws/

Ahora se hará un caktin_make, que es una herramienta de línea de comandos que agrega cierta comodidad al flujo de trabajo.

>catkin_make

Ahora se hará un source que permite ver los archivos dentro del entorno y ponerlos disponibles para el operario.

>source devel/setup.bash

Con el siguiente comando podras descubir donde se encuentra la caperta de ros.

>echo $ROS_PACKAGE_PATH

Para poder aclarar cosas en la consola se considera el siguiente paso.

>vi ./bashrc

En la que se baja la última parte de la lista y se agrega en este caso, la siguiente informaicón como tipo de versión en la que se encuentra. Se sugiera las siguientes listas de comandos.

Considere que aespis es el usuario del ordanador y noetic la versión con la que se esta trabajando.

>ROS_VERSION="Noetic"

>echo "ROS version" $ROS_VERSION

>source /opt/ros/noetic/setup.bash

>source /home/aespis/catkin_ws/devel/setup.bash

Lo último, para dejar lo cambios se presiona la tecla "Esc" y se agrega el comando :wq. (Dicho comando es para guardar los cambios)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/a7d39b15-98d8-41d0-85bd-d44119931a6b)


2. Crear un ejemplo basico de publish/subscribe y compilar

Ahora para iniciar se da como consejo que la carpeta donde se ejecuta todo, la cual es caktin_ws, no sea la capa principal si no la siguiente por ende, para hacer este paso se hace lo siguiente.

Se va la carpeta la cual se quiere hacer que sea la siguiente capa.

>cd catkin_ws

>cat devel/setup.bash

>source devel/setup

Para este ejemplo, se descargan directamente de la página de ros los tutoriales.

>https://wiki.ros.org/ROS/Tutorials

Para el ejemplo básico se iniciar ros tutorials. (Estos tienen unos tutoriales dentro la página a seguir, pero se va hacer con otro tipo de ejemplo)

>sudo apt-get install ros-noetic-ros-tutorials

Se instala la cámara, dentro de ella la que viene por defecto de ros.

>sudo apt-get install ros-noetic-usb-cam

Ahora se llama a la cámara para este es

>roslaunch usb_cam usb_cam-test.launch

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/0b523c37-f968-4181-8821-ed3a8ebdb68e)

Por lo tanto para ver si se encuentra dichos comandos del roslaunch, se ejecuta los siguientes comandos para ver que se encuentra en el momento de encender la cámara, tales comandos son.

>rostopic list

>rosnode list

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/96080233-80ba-41fe-8b2e-7c19a4d63055)

El roslaunch, ejecuta el roscore por lo que se puede apreciar que es un ejemplo de suscripción ya que actua la cámara como el publicador, esperando en esta caso el nodo para mirar la info. Como se aprecia en gráfico de la imagén.

Para comprobar se ejecutará el siguiente comando.

>rosnode info /image_view 

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/b48956b4-325a-48a6-88a9-5af94c1f6c5e)

>rosnode info /usb_cam

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/215892fa-b306-4569-840f-a07c00c91779)

Podemos también comprobar los nodos, de la siguiente manera. Comprobando que esta enviando /usb_cam/imag_raw

>rostopic echo /usb_cam/image_raw

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/fa8e7719-a4fd-4dd8-9091-03dc9373ff6e)


3. Probar todos los ejemplos de publish/subscribe del repositorio asociado.

Se descarga los ejemplos en este caso del link asociado y se va a la carpeta correspondiente.

Una vez descargado, se debe hacer un catkin_make dentro de la carpeta src/. (Dentro de la carpeta src/, se debe añadir todos las carpetaas descargadas)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/1d797451-1190-4082-9707-4c30590ec029)

Se ejecuta el launch predefinido. (roslaunch)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/007970f9-d0b6-4c02-989b-8700ef81a6b3)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/e1ffe872-e1c4-4a59-85cc-e2978f3cb477)


5. Compilar con catkin make y compilar con catkin build [1].

Para poder compilar con caktin build, se recomienda seguir el siguiente link:

>https://catkin-tools.readthedocs.io/en/latest/verbs/catkin_build.html

7. Revisar y comparar el espacio de trabajo en cada caso.

Sólo quiero añadir que cree está carpeta pero con en la carpeta catkin_ws, me sale un error diciendo que como ya compile con el comando catkin_make, debe ser que al seleccionar sólo una al momento de crear un carpeta.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/3be26d3a-994f-420e-8906-b72ff12b5dcf)


9. Entender las diferencias entre las carpetas source, install, devel, build, y result.

source:

Propósito: En términos sencillos, podríamos comparar la carpeta 'source' con el taller de un artista. Aquí es donde reside la esencia creativa del paquete, ya que almacena el código fuente, scripts de compilación y archivos de configuración. Es el espacio donde los desarrolladores dan forma y modifican sus creaciones.

Contenido: Esta carpeta alberga los archivos que conforman el ADN del paquete: el código fuente que los desarrolladores crean y manipulan para construir su aplicación. Además, incluye scripts de compilación que son esenciales para transformar este código en una forma ejecutable, junto con archivos de configuración que ajustan el comportamiento del sistema.

Notas adicionales: Es el corazón del proceso de desarrollo, donde los programadores dan rienda suelta a su creatividad, escribiendo y modificando código para construir la base de su aplicación.

install:

Propósito: Después de que los artistas han terminado de trabajar en su taller (carpeta 'source'), es hora de mostrar su obra al mundo. 'Install' es como la galería de arte donde se exhiben las creaciones, pero en el mundo de la programación. Aquí es donde se copian los resultados finales después de compilar el código fuente.

Contenido: En 'install' se encuentran los ejecutables, bibliotecas y archivos de configuración que constituyen la versión ejecutable del paquete. Es como el catálogo de una exposición, mostrando los elementos finales listos para su uso.

Notas adicionales: Esta carpeta se utiliza comúnmente para crear un entorno de ejecución separado del entorno de desarrollo. Es el espacio donde el paquete cobra vida y se ejecuta de manera independiente.

devel:

Propósito: Similar a 'install', pero más como el backstage de un espectáculo. La carpeta 'devel' contiene los elementos necesarios durante el desarrollo mismo. Aquí se encuentran los archivos compilados y otros recursos que permiten ejecutar el código directamente desde el espacio de desarrollo, evitando la necesidad de instalar el paquete.

Contenido: Ejecutables, bibliotecas y archivos de configuración también residen en 'devel', pero son utilizados específicamente para facilitar la depuración y la ejecución de código que aún no ha sido instalado.

Notas adicionales: Esta carpeta es como el estudio del artista donde las ideas están en constante evolución. Facilita el proceso creativo al proporcionar un entorno dinámico para el desarrollo y las pruebas.

build:

Propósito: Imagina 'build' como el taller temporal que se monta para fabricar las piezas de una obra de arte. Esta carpeta contiene los archivos generados durante el proceso de compilación, como objetos intermedios y archivos de configuración temporales.

Contenido: Archivos temporales y generados durante la construcción del paquete. Estos son elementos necesarios para el proceso de compilación, pero no son parte del producto final.

Notas adicionales: Después de una exitosa compilación, esta carpeta puede ser eliminada para mantener limpio el espacio en disco, ya que su contenido temporal ya ha cumplido su propósito.

result:

Propósito: En este caso, 'result' es como el archivo de críticas y reseñas después de una exposición de arte. Contiene los resultados específicos del paquete después de su ejecución, como archivos de registro, resultados de pruebas y otras salidas específicas.

Contenido: Archivos que documentan y detallan los resultados y el rendimiento del paquete después de haber sido ejecutado.

Notas adicionales: A diferencia de las carpetas anteriores, 'result' no es estándar en todos los paquetes y su presencia y contenido pueden variar según la configuración y los requisitos específicos del paquete. Es como el informe crítico después de una actuación, proporcionando información valiosa sobre el desempeño del paquete.

11. Modificar el ejemplo de publish subscribe que has generado para que se produzcan esperas en la gestion de 
los callbacks.

Se basa en el ejemplo del siguiente canal de Youtube.

>https://www.youtube.com/watch?v=_lmtdNaHDZA&list=PLCnFMDeQwi_qu2DfKmpG5ddKtbdKdfMCw&index=7&ab_channel=RodolfoCuan

Para ello lo primero es crear una carpeta donde se almacenara un publisher y susbriber, para eso se recomienda en la carpeta src/, crear dicha carpeta.

> cd catkin_ws/src/

>catkin_create_pkg ejemplos roscpp rospy std_msgs

>mkdir pub_sub

>touch topic_publisher.py

Luego para modicar ese py, se hace el siguiente comando.

>gedit topic_publisher.py

La cual abrira en este caso el editor de texto y se copia lo siguiente.

#!/usr/bin/env python

import rospy

from std_msgs.msg import Int32

rospy.init_node('publisher_node')

pub = rospy.Publisher('counter', Int32, queue_size=1)

rate=rospy.Rate(15) #Hz del mensaje

count=0

while not rospy.is_shutdown():
   pub.publish(count)
   count += 1
   rate.sleep()  #Dilay para la frecuencia que indicamos.

Luego necesitamos que el archivo sea ejecutable, para ello se hace el sigbuiente comando.

>sudo chmod u+x topic_publisher.py 

Luego hacer un source, en la carpeta de catkin_ws.

>source devel/setup.bash

Se corre un roscore, para ver si el nodo sirve. 

>roscore

En otra terminal ejecutamos lo siguiente.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/19cd1d44-bac6-4aa9-8c71-571144fed8dd)

Ahora falta crear el nodo suscriptor.

Para ello se implementa los mismo hasta el touch, pero ya no es necesario más carpeta, en la creada se puede hacer el mismo ejemplo.

>touch topic_subscriber.py

>gedit topic_suscriner.py

#!/usr/bin/env python

import rospy
from std_msgs.msg import Int32  # Corregir la importación de Int32

def callback(msg):
    rospy.sleep(10)  # Esperar 10 segundos antes de imprimir el mensaje
    print(msg.data)

rospy.init_node("subscriber_node")  # Corregir el nombre del nodo
sub = rospy.Subscriber("counter", Int32, callback)  # Corregir el tipo de mensaje

rospy.spin()  # Agregar esto para mantener el programa en ejecución

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/30edae16-c6cb-461d-9dfd-2f5ba458058d)


13. Modificar los nodos para que en las mismas circunstancias funcione.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/906c8fa3-24a7-4507-860a-af86e9911d59)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/14c3f773-3730-4dd1-b020-d418674e7880)

15. Revisar el funcionamiento de ROSlint y entender como se despliega y ejecuta.

ROSlint es una herramienta de análisis estático para linting de código en el contexto de ROS (Robot Operating System). Se utiliza para verificar y mejorar la calidad del código fuente en paquetes ROS, aplicando reglas y estándares de estilo específicos para C++ y Python.

Dependencia de Compilación:

Se agrega una dependencia de compilación en el archivo package.xml del paquete ROS

> <build_depend>roslint</build_depend

Configuración en CMakeLists.txt:

En el archivo CMakeLists.txt, se incluye ROSlint como una de las dependencias de catkin:

>find_package(catkin REQUIRED COMPONENTS roslint ...)

Invocación de ROSlint en CMakeLists.txt:

Se invoca la función ROSlint desde el archivo CMakeLists.txt:

>roslint_cpp()

Ejecución de ROSlint:

Para ejecutar ROSlint en el paquete, se utiliza catkin_make con el objetivo roslint del paquete:

>catkin_make roslint_my_fancy_package
