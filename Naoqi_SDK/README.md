# Instalación SDKs

Toda la información será registrada en este documento acerca de SDKs. Por lo tanto, se dará los links y pasos a seguir.

1.  Ingresar al siguiente link.

    • https://www.aldebaran.com/en/support/nao-6/downloads-softwares

En la sección SDKs, hacer clic en Former versions.
![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/1932815c-07a9-4ebe-99e1-cb886843dac1)

Una vez dentro, se debe descargar las dos versiones que se muestra en la imagen, de tal manera que una podrá ejecutar el código en c++ y la otra en python.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/402b0e5f-2933-4e61-a8d3-8b83043e2bfc)

2. Ejecución vía terminal para descargas.

Para esto debemos ejecutar el terminal y comprimir las carpetas previamente descargas ó en su defecto descomprimirlas.

Para comprimir mediante código es:

Descargas o sitio donde se guardo la carpetas

    > cd directory 

Para descomprimir desde código es el siguiente comando, teniendo en cuenta que “carpeta” es el nombre de como se guardo el documento previamente descargado.

    > tar xvfz carpeta

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/065655dc-4772-48c9-8511-c7bfd34262d8)


Una  vez descargada, debe apareces de la siguiente manera.

3.Ejecución de Carpetas.

Se ejecuta de la carpeta de naoqi el mismo ejecutable del mismo nombre.

    > ./naoqui

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/4cbf8b3b-a516-43f1-a408-d0e3d0fdbfbb)

Se acaba de levantar el core de naoqi.

Ahora para ejecutar el service, se va directamente a la documentación de naoqi para seguir el ejemplo que ofrece el proveedor.

    > http://doc.aldebaran.com/2-4/dev/libqi/guide/py-service.html

Para la ejecución del como escribir un qumessaging service, se debe hacer mediante dos textos .py los cuales tendrán el servicio y el testeo de este. Por ende, se procede a crear una carpeta con los contenidos previamente mencionados.

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/fcad1f0b-d2a1-497a-9fd3-ef5d7a948c21)

Considere que dentro de la carpeta Service.py se encuentra el siguiente código.

```
import qi

class MyFooService:
  def __init__(self, *args, **kwargs):
    #define a signal 'onBang'
    self.onBang = qi.Signal()

  #define a bang method that will trigger the onBang signal
  def bang(self):
    #trigger the signal with 42 as value
    self.onBang(42)
    
import qi
import sys

#create an application
app = qi.Application(sys.argv)
app.start()

#create an instance of MyFooService
myfoo = MyFooService()

s = app.session
#let's register our service with the name "foo"
id = s.registerService("foo", myfoo)

#let the application run
app.run()
```
Del cual se encuentra en link previamente mencionado. (Los paréntesis  en el print es porque se va a lanzar en python 3, que obliga a este comando que dicha información este dentro los paréntesis)

En la carpeta Client.py, se encuentra el siguiente código.


```

import qi
import sys

def onBangCb(i):
  print ("bang:", i)

app = qi.Application(sys.argv)
app.start()
s = app.session
foo = s.service("foo")

#register a callback on 'onBang'
foo.onBang.connect(onBangCb)
#call bang
foo.bang()

```

4. Ejecutar el Service.

Para esto se considerá hacer los siguientes pasos. 

Primero se ingresa a la carpeta donde se encuentra el Service.py y el Client.py. De los cuales, se ejecutan mediante python.

    > Pyhton3 Service.py
    
    > Pyhton3 Client.py

![image](https://github.com/andresfespinosas/Masters-in-Robotics-and-IA-University-of-Leon./assets/128443182/d0aeeded-cec7-4aa8-aeb8-a6697a5774e0)


