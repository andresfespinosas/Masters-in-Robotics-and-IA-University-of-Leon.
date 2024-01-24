![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/5a0a48ee-c6f5-45ec-9a70-17ac2684c662)Lo primero está basado en el siguiente repositorio.

> https://github.com/robotology/yarp

En una carpeta, se hará git clone.

>git clone https://github.com/robotology/yarp

>cd yarp/docker

>docker build . -f Dockerfile -t yarp:test

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/39f14bd0-d49e-4146-834d-f3a0856f9aae)

Luego se hará un sudo python-rocker,

>sudo apt-get install python3-rocker

Dentro del cd previamente se ejecuta el siguiente código.

>docker run -it yarp:test

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/dd436e3a-1167-4a5e-b169-4f2721c6ca74)

El primer ejemplo según la página oficial.

>https://www.yarp.it/latest/companion_use.html

Antes que nada, se ejecuta el yarp server.

>yarp server

Se crea el primer puerto en otra terminal.

>>docker exec -it 349d4b21cb0c /bin/bash 

>yarp read /port1

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/8db6dde9-ced7-49f4-a5df-0a66a102751d)

Luego en la siguiente terminal.

>docker ps -a

Se mira el ID del contenedor bin/bash

>docker exec -it 349d4b21cb0c /bin/bash 

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/4793c247-8dbf-43dd-8608-177168058560)

>yarp write /port2 /port1

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/1ad2d013-e4be-4314-b8d7-5ab35feb8228)


Si sólo se quiere escribir en el último comando es decir

>yarp write /port2

En otro termianl, se conecta como todos y se pone lo siguiente

>yarp connect /port2 /port1

