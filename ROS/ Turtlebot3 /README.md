Ejercicios TurtleBot3

1. Instalar el simulador de Turtlebot 3 y probarlo.

De acuerdo a la página oficial de TurtleBot3, en la sección de Simulación.

>https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation

Instalar el paquete de simulación

>cd ~/catkin_ws/src/

>git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

>cd ~/catkin_ws && catkin_make

Para exportar los turtlebot3, hay 3. De los cuales con el código se exporta uno diferente.

>export TURTLEBOT3_MODEL=burger

>export TURTLEBOT3_MODEL=waffle

>export TURTLEBOT3_MODEL=waffle_pi

Recomendación: Debe seleccionar un solo modo y una vez escogido este modelo debe insertalo al principio de cualquier terminal ya que si se quiere lanzar otro turtlebot es sólo exportar uno de los 3.

También cuenta con 3 mapas diferentes, en los que se mustra según el documento oficial.

>roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch

>roslaunch turtlebot3_gazebo turtlebot3_world.launch

>roslaunch turtlebot3_gazebo turtlebot3_house.launch

Las imagenes de cada uno se encuentra en la página oficial.

Ahora para desplegar por dar un ejemplo sería la siguiente manera, en la terminal entrar en la carpeta creado según esta guía catkin_ws/src

>cd catkin_ws/src

>export TURTLEBOT3_MODEL=burger

>roslaunch turtlebot3_gazebo turtlebot3_house.launch

En otra terminal con el mismo espacio de caktin_ws/src, para poder en este caso teleperarlo. Se ejecuta en el siguiente código:

>roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/15fd8bd7-f6ca-41de-bf8b-9a45c3c15749)


2. Desplegar los ejemplos de navegacion del repositorio de prácticas. 

Desplazamiento por velocidad.

Desplazamiento un intervalo de tiempo.

Desplazamiento a un punto utilizando odom.

Para desplegar este launcher, se debe descargar el repositorio y ponerla en la carpeta src de tú carpeta de preferencia.

En este caso se ejecuta de la siguiente manera.

>cd catkin_ws/src

>roslaunch laboratorios-andresfespinosas-main/simple_navigation_ros/launch/example.launch 

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/786d357d-a309-40bc-8444-ef1b4e3dc40a)

Lo único es empezar a mapear todo el mapa, para ello se recomuienda ir con el roboto a los sitios que se desee.

3. Generar un mapa con gmapping en el simulador del mundo .

$ roslaunch turtlebot3 gazebo turtlebot3 world.launch

Para esto se ejecuta el siguiente comando, considerando el turtlebot que tienes ejecutado en comando.

>export TURTLEBOT3_MODEL=burger

>roslaunch turtlebot3_slam turtlebot3_slam.launch

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/ec79c5f1-4a86-4f37-9bd5-2509c6624564)

4. Dibujar el arbol de transformadas y explicar su estado.

Lo priemro es hacer un install de las trasnformadas.

>sudo apt install ros-noetic-tf2-tools

Una vez instalada, se ejeucta el código correspondiente.

>rosrun tf2_tools view_frames.py

Esto genera un pdf, para ello se vusca en el directorio. (Es una manera o hacer echo a este)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/59aae903-6a63-47a4-a90f-e58c8772ee0b)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/84546c9f-11b7-4f84-8d4e-786a8c4ae1fa)

Luego se examina.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/c922888d-169c-47fc-a3e2-4ab310b2120f)

Entonces el explica, primero donde se encuentra, que sería el map, luego el odom  que es el encargado de ubicarse donde se encuentra dentro de mapa para ello luego sigue el base link, que es la forma física del robot, en este cago es un burguer, a parte de la base link que sería como esta constituido dicho robot, que sus siguientes compoenentes o elementos, tales como ruedas o sus sensores.
