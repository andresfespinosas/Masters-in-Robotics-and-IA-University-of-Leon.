1. Generar un mapa con karto en el simulador con el mundo House de Gazebo.

$ roslaunch turtlebot3 gazebo turtlebot3 house.launch

2. Realizar el tutorial de el sistema de generacion de trayectorias ´ TEB.

Sustituir el DWA por TEB y probar su uso

Extra para subir nota. Probar los launch disponibles en el tutorial

3. Crear un nodo de ROS para gestionar la navegacion a un punto establecido del apartamento. ´


4. Crear un nodo ROS que haga navegar al Turtlebot entre waypoints (WP) predefinidos le´ıdos desde un fichero
yaml que contendra coordenadas definidas sobre el mapa ´ House de Gazebo.


5. El nodo de navegacion deber ´ a tener tres modos de funcionamiento que se activar ´ an mediante servicios: ´
Regular: el robot navega en secuencia entre los WPs definidos en el fichero (mismo funcionamiento del
ultimo paso anterior). ´
Aleatorio: el robot navega de forma aleatoria entre WPs.
Espera: el robot no hace nada.
