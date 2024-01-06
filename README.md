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

>cd basic_ros/



5. Compilar con catkin make y compilar con catkin build [1].



7. Revisar y comparar el espacio de trabajo en cada caso.


9. Entender las diferencias entre las carpetas source, install, devel, build, y result.


11. Modificar el ejemplo de publish subscribe que has generado para que se produzcan esperas en la gestion de 
los callbacks.


13. Modificar los nodos para que en las mismas circunstancias funcione.


15. Revisar el funcionamiento de ROSlint y entender como se despliega y ejecuta.
