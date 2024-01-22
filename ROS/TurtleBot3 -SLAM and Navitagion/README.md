![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/44073dc1-5a70-44c7-8e33-5045169a14c1)1. Generar un mapa con karto en el simulador con el mundo House de Gazebo.

$ roslaunch turtlebot3 gazebo turtlebot3 house.launch

Antes del roslaunh recodar exportar el modelo.

>export TURTLEBOT3_MODEL=burger

2. Realizar el tutorial de el sistema de generacion de trayectorias ´ TEB.

Primero se hace la generación del SLAM para trayectorias.

En una terminal aparte, se veulve a exportar el modelo 

>export TURTLEBOT3_MODEL=burger

Luego sigue lanzar el slam, gmapping.

>roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

Para luego con un comando para teleoperarlo y mapear el mapa (En otra terminal)

>export TURTLEBOT3_MODEL=burger

>roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

Una vez se tenga todo el mapa, se ejecuta el siguiente código.

> rosrun map_server map_saver -f ~/mapa

Para modificarlo se recomienda el siguiente programa.

>gimp mapa.pgm

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/5315261d-d072-4b08-b04a-05acdc38e8cd)


3. Crear un nodo de ROS para gestionar la navegacion a un punto establecido del apartamento. ´

Se recomienda la siguiente modifica una vez ejecuta de nuvo el mapa y gazebo.

>roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/mapa.pgm

El siguiente es:

>rosrun rqt_reconfigure rqt_reconfigure

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/24bd11f4-dc61-495d-91e6-2b9deb480cd6)

Lo primero es crear una carpeta donde se encontrara los nodos de todos los puntos en este caso se recomienda el siguiente procedimiento.

>cd catkin_ws/src

>catkin_create_pkg my_navigation_pkg rospy nav_msgs actionlib

Se crea dentro de esta carpeta los nodos correspondiente a cada ejercicio, para el primero.

>cd catkin_ws/src/my_navigation_pkg

>touch point_navigation_node.py

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/dca8f3b3-12f7-4cca-98f4-0be052282f8c)

```
#!/usr/bin/env python

import rospy
from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
import actionlib


def move_to_goal(x, y):
    # Inicializar el nodo
    rospy.init_node('nodo_navegacion', anonymous=True)

    # Crear un cliente para move_base
    client = actionlib.SimpleActionClient('move_base', MoveBaseAction)
    client.wait_for_server()

    # Crear un goal para move_base
    goal = MoveBaseGoal()
    goal.target_pose.header.frame_id = "map"
    goal.target_pose.header.stamp = rospy.Time.now()

    # Establecer la posición del objetivo
    goal.target_pose.pose.position.x = x
    goal.target_pose.pose.position.y = y
    goal.target_pose.pose.orientation.w = 1.0

    # Enviar el goal a move_base y esperar la respuesta
    client.send_goal(goal)
    client.wait_for_result()

    # Imprimir el resultado de la acción
    result = client.get_result()
    rospy.loginfo(f"Resultado de la navegación: {result}")

if __name__ == '__main__':
    try:
        # Especificar las coordenadas del punto de destino
        target_x = 6.0   #Eje x
        target_y = 0.9   #Especifica las coordenadas.

        # Llamar a la función para moverse al objetivo
        move_to_goal(target_x, target_y)

    except rospy.ROSInterruptException:
        rospy.loginfo("Navegación interrumpida")
        
```

Por último para preparar el código

>chmod +x ~/catkin_ws/src/my_navigation_pkg/point_navigation_node.py

Se ejecuta en una terminal.

>rosrun my_navigation_pkg point_navigation_node.py

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/b1a0ed6a-e15a-466f-9626-79c22ad6fc80)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/0c4af8a3-1a81-45d8-a4ea-6588aee562ac)

4. Crear un nodo ROS que haga navegar al Turtlebot entre waypoints (WP) predefinidos le´ıdos desde un fichero
yaml que contendra coordenadas definidas sobre el mapa ´ House de Gazebo.

Lo primero es crear un hoja yaml, donde se pondra los waypoints.

>cd catkin_ws/src/my_navigation_pkg

>touch waypoints.yaml

Dentro de esta carpeta.

waypoints:
  - name: sala
    coordinates: [6.0, -0.9]

  - name: comedor
    coordinates: [6.15, 3.3]

  - name: habitacion
    coordinates: [1.0, 4.7]

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/236a83f3-08ee-4f04-80c9-212144b2e8fc)

Lo siguiente es crear el py. No se dará el proceso por que para eso se aconseja mirar el punto anterio, sólo que este nodo de se llamará nodo_nav_py.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/5531288d-1599-4a0f-aae5-fe954bc9d423)


![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/b9542a13-1659-4a10-aead-57bed70940b1)

```

#!/usr/bin/env python

import os
import rospy
from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
import actionlib
import yaml

def read_waypoints_from_yaml(file_path):
    with open(file_path, 'r') as stream:
        try:
            waypoints_data = yaml.safe_load(stream)['waypoints']
            waypoints_list = []

            for waypoint_entry in waypoints_data:
                print (waypoints_data)
                waypoint = {
                    'name': waypoint_entry['name'],
                    'x': waypoint_entry['coordinates'][0],
                    'y': waypoint_entry['coordinates'][1]
                }
                waypoints_list.append(waypoint)

            return waypoints_list

        except yaml.YAMLError as e:
            rospy.logerr(f"Error al leer el archivo de waypoints: {e}")
            return []

def move_to_waypoint(waypoint):
    # Inicializar el nodo
    rospy.init_node('nodo_navegacion', anonymous=True)

    # Crear un cliente para move_base
    client = actionlib.SimpleActionClient('move_base', MoveBaseAction)
    client.wait_for_server()

    # Crear un goal para move_base
    goal = MoveBaseGoal()
    goal.target_pose.header.frame_id = "map"
    goal.target_pose.header.stamp = rospy.Time.now()

    # Establecer la posición del objetivo
    goal.target_pose.pose.position.x = waypoint['x']
    goal.target_pose.pose.position.y = waypoint['y']
    goal.target_pose.pose.orientation.w = 1.0

    # Enviar el goal a move_base y esperar la respuesta
    client.send_goal(goal)
    client.wait_for_result()

    # Imprimir el resultado de la acción
    result = client.get_result()
    rospy.loginfo(f"Navegación al waypoint {waypoint['name']} - Resultado: {result}")

if __name__ == '__main__':
    try:
        # Obtener el directorio actual
        directorio_actual = os.getcwd()

        # Imprimir el directorio actual
        rospy.loginfo(f"El directorio actual es: {directorio_actual}")

        # Obtener la lista de waypoints desde el archivo YAML
        waypoints_file_full_path = os.path.join(directorio_actual, "waypoints.yaml")
        waypoints = read_waypoints_from_yaml(waypoints_file_full_path)

        if not waypoints:
            rospy.logerr("No se pudieron cargar los waypoints. Verifica el archivo YAML.")
            exit()

        # Navegar a cada uno de los waypoints
        for waypoint in waypoints:
            move_to_waypoint(waypoint)

    except rospy.ROSInterruptException:
        rospy.loginfo("Navegación interrumpida")

```
Se recomienda ejecutar este rosrun dentro de la carpeta donde se encuentre el yaml de waypoints.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/af603b8a-7d52-4be6-806c-034cfd9f191f)

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/538217bc-ea0e-4ea1-b285-88651a1c17f3)


5. El nodo de navegacion deber ´ a tener tres modos de funcionamiento que se activar ´ an mediante servicios: ´
Regular: el robot navega en secuencia entre los WPs definidos en el fichero (mismo funcionamiento del
ultimo paso anterior). ´
Aleatorio: el robot navega de forma aleatoria entre WPs.
Espera: el robot no hace nada.

Se recuerda otra vez, realizar un py. En esta caso nodo_control.py

```
#!/usr/bin/env python

import rospy
from std_srvs.srv import Empty, EmptyResponse
from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
import actionlib
import yaml
import os
import random

class NodoServicios:
    def __init__(self, nodo_control):
        # Guardar referencia al nodo_control
        self.nodo_control = nodo_control

        # Crear servicios para cambiar modos de funcionamiento
        rospy.Service('modo_navegacion_secuencia', Empty, self.modo_navegacion_secuencia)
        rospy.Service('modo_navegacion_aleatorio', Empty, self.modo_navegacion_aleatorio)
        rospy.Service('modo_navegacion_espera', Empty, self.modo_navegacion_espera)

    def modo_navegacion_secuencia(self, request):
        rospy.loginfo("Modo de navegación cambiado a secuencia")
        self.nodo_control.set_modo("secuencia")
        return EmptyResponse()

    def modo_navegacion_aleatorio(self, request):
        rospy.loginfo("Modo de navegación cambiado a aleatorio")
        self.nodo_control.set_modo("aleatorio")
        return EmptyResponse()

    def modo_navegacion_espera(self, request):
        rospy.loginfo("Modo de navegación cambiado a espera")
        self.nodo_control.set_modo("espera")
        return EmptyResponse()

class NodoControl:
    def __init__(self):
        # Crear un cliente para move_base
        self.move_base_client = actionlib.SimpleActionClient('move_base', MoveBaseAction)
        self.move_base_client.wait_for_server()

        # Obtener el directorio actual
        directorio_actual = os.getcwd()

        # Imprimir el directorio actual
        rospy.loginfo(f"El directorio actual es: {directorio_actual}")

        # Obtener la lista de waypoints desde el archivo YAML
        waypoints_file_full_path = os.path.join(directorio_actual, "waypoints.yaml")
        self.waypoints = self.read_waypoints_from_yaml(waypoints_file_full_path)

        # Verificar si no se pudieron cargar los waypoints
        if not self.waypoints:
            rospy.logerr("No se pudieron cargar los waypoints. Verifica el archivo YAML.")
            exit()

        self.servicio_llamado = False
        self.modo = "espera"  # Establecer un valor predeterminado
        self.waypoints_secuencia = []  # Almacena la secuencia de puntos para el modo secuencia
        self.indice_secuencia = 0  # Índice actual en la secuencia de puntos
        self.waypoints_aleatorio = []  # Almacena la lista de waypoints para el modo aleatorio
        self.waypoints_1 = []     

        # Crear la lista de waypoints para el modo aleatorio
        if 'waypoints' in self.waypoints:
            self.waypoints_1 = self.waypoints['waypoints']
            

    def set_modo(self, modo):
        self.modo = modo
        self.servicio_llamado = False  # Establecer la bandera a False al cambiar el modo

    def ejecutar(self):
        try:
            rate = rospy.Rate(1)  # 1 Hz
            while not rospy.is_shutdown():
                if self.modo == "secuencia":
                    self.navegacion_secuencia()
                elif self.modo == "aleatorio":
                    self.navegacion_aleatoria()
                elif self.modo == "espera":
                    self.modo_espera()

                rate.sleep()

        except rospy.ROSInterruptException:
            pass

    def navegacion_secuencia(self):
        rospy.loginfo("Ejecutando navegación en secuencia...")
        while not rospy.is_shutdown() and not self.servicio_llamado and self.modo =="secuencia":
            if self.waypoints_1:
                waypoint = self.waypoints_1[self.indice_secuencia]
                rospy.loginfo(f"Navegando hacia el waypoint: {waypoint['name']}")
                self.navegar_hacia_punto(waypoint['coordinates'])

                # Incrementar el índice y volver al principio si es necesario
                self.indice_secuencia = (self.indice_secuencia + 1) % len(self.waypoints_1)

        # Restablecer el servicio llamado al final de la secuencia
        self.servicio_llamado = False

    def navegacion_aleatoria(self):
        rospy.loginfo("Ejecutando navegación aleatoria...")
        while not rospy.is_shutdown() and not self.servicio_llamado and self.modo =="aleatorio":
            # Seleccionar un waypoint aleatorio diferente al actual
            nuevo_indice = self.indice_secuencia
            while nuevo_indice == self.indice_secuencia:
                nuevo_indice = random.randint(0, len(self.waypoints_1) - 1)

            waypoint = self.waypoints_1[nuevo_indice]
            rospy.loginfo(f"Navegando hacia el waypoint aleatorio: {waypoint['name']}")
            self.navegar_hacia_punto(waypoint['coordinates'])

        # Restablecer el servicio llamado al final de la navegación aleatoria
        self.servicio_llamado = False

    def modo_espera(self):
        stop_pub = rospy.Publisher('/move_base/cancel', MoveBaseGoal, queue_size=1)
        stop_msg = MoveBaseGoal()
        stop_pub.publish(stop_msg)
        rospy.loginfo("Modo cambiado a espera")
        while not rospy.is_shutdown() and not self.servicio_llamado and self.modo =="espera":
            rospy.sleep(0.1)  # Esperar hasta que se reciba un nuevo servicio o se cierre el nodo

    def navegar_hacia_punto(self, coordinates):
        # Implementa la lógica para enviar una meta a move_base
        goal = MoveBaseGoal()
        goal.target_pose.header.frame_id = "map"
        goal.target_pose.pose.position.x = coordinates[0]
        goal.target_pose.pose.position.y = coordinates[1]
        goal.target_pose.pose.orientation.w = 1.0

        rospy.loginfo("Enviando meta a move_base...")
        self.move_base_client.send_goal(goal)

        # Esperar hasta que la acción se complete o el modo cambie
        #while not rospy.is_shutdown() and not self.servicio_llamado:
        result = self.move_base_client.get_result()
        modo_actual = self.modo
        while not result and modo_actual == (self.modo):
            result = self.move_base_client.get_result()
            rospy.sleep(0.1)  # Esperar 0.1 segundos antes de verificar nuevamente

        if result:
            rospy.loginfo(f"Resultado de la navegación: {result}")
            
        else:
            rospy.logwarn("No se pudo obtener el resultado de la navegación.")

    def read_waypoints_from_yaml(self, file_path):
        try:
            with open(file_path, 'r') as file:
                waypoints = yaml.safe_load(file)
                return waypoints
        except FileNotFoundError:
            rospy.logerr(f"El archivo {file_path} no se encuentra.")
            return None
        except Exception as e:
            rospy.logerr(f"Error al leer waypoints desde {file_path}: {e}")
            return None

if __name__ == '__main__':
    rospy.init_node('nodo_control', anonymous=True)
    nodo_control = NodoControl()
    nodo_servicios = NodoServicios(nodo_control)
    nodo_control.ejecutar()
    rospy.spin()

```
No pondra imagenes del código por motivo de que esta extenso.

Pero si unos pantallasos del modo espera y aleatorio...

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/c48cf399-e99c-485d-84a6-8dc448a9520b)

Se puede ver claramente que estaba en aletroio y paso a modo espera, en la imagen no se aprecia pero se quedo quieto y mantiene la ruta previmaente definida que era aleatoria.

