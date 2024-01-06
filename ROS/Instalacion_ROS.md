# Web Original:
 >https://wiki.ros.org/es/ROS/Installation

Cómo sistemas de Base hay para Kinetic, Melodic y Noetic. (Todas soportadas por su actulización, de tal que, de acuerdo al sistema opertativo se elige una de las mencionadas.)

>ROS Kinetic Kame :  https://wiki.ros.org/es/kinetic/Instalacion 

>ROS Melodic Morenia : https://wiki.ros.org/es/kinetic/Instalacion

>ROS Noetic Ninjemys : https://wiki.ros.org/noetic/Installation

Cada una con su plataforma correspondiente.

## En este caso particular se usa ROS Noetic - Ubuntu.

**1. Instalación**

 Configure su computadora para aceptar software de packages.ros.org

 >sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

 Configurar llaves

 >sudo apt install curl # if you haven't already installed curl curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

 Actualizar Debian
 
 >sudo apt update

 Instalar paquetes recomendados.
 
 >sudo apt install ros-noetic-desktop-full

 Es importante conocer que los paquetes se encuentren en la carpeta.

 >apt search ros-noetic

También debe obtener el script en cada terminar bash de que ROS está.

>source /opt/ros/noetic/setup.bash

Dependecias para paquetes.

>sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential

Inicialización de rosdep

>sudo apt install python3-rosdep

>sudo rosdep init

>rosdep update

