# ExamenPracticoSistemas

## 1.Introducción

Mi proyecto trata de una aplicación destinada a la gestión de stock y almacenes llamada GAI.

Primero instalaremos docker-compose dirigiéndonos a la consola y introduciendo el comando `sudo apt install docker-compose` 

![image](https://user-images.githubusercontent.com/91564872/172453616-d6ff7369-5903-4b01-8a52-b5730c37fca5.png)


## 2.Configuración del archivo docker-compose.yml

Primer nos dirigiremos a la consola y mediante el comando `touch docker-compose.yml` crearemos el archivo

![image](https://user-images.githubusercontent.com/91564872/172448561-caa60784-400c-4eb4-801b-fbd0a961c446.png)

A continuación, crearemos un directorio nuevo que llamaremos "DOCKER" para introducir todos los archivos necesarios:

![image](https://user-images.githubusercontent.com/91564872/172448999-e487dd26-e720-4f0b-9928-5ceb13f0dc93.png)

En esta carpeta tambien introduciremos el archivo `.war` de nuestro proyecto.

![image](https://user-images.githubusercontent.com/91564872/172453973-22343416-ccc9-41c0-bb30-935653f326d8.png)


Ahora modificaremos el archivo .yml de la siguiente manera:

![image](https://user-images.githubusercontent.com/91564872/172452469-8778260b-6478-441e-af83-7db1f98b37ac.png)

Primero declararemos las imagenes que vamos a usar como se puede ver en `image:` que en este caso son tomcat, MySQL y phpmyadmin. 

Tomcat y phpmydamin dependen de la base de datos es decir de mysql, así que será la primera que configuraremos. En `volume:` le daremos las indicaciones para que ejecute nuestra base de datos desde MySQL al iniciarse. A continuación usaremos `environment:` para declarar el usuario root, su contraseña y el nombre de la base de datos que queremos iniciar. Finalmente en `ports:` le asignaremos el puerto que va ocupar, en este caso el 3306:3306.

Pasamos a phpmyadmin. Tras declarar que depende de la base de datos y la declaración de `image:` que nos sirve para indicar que imagen descargaremos y configuraremos, le asignaremos su puerto mediante `ports:` que en este caso es el 8081:80. Finalmente usaremos `environment:` como he mencionado anteriormente para declarar la contraseña del usuario root. Es muy importante recordar esta contraseña ya que sino luego no podremos utilizar el phpmyadmin.

Finalmente con tomcat, declararemos su dependencia de la base de datos, en `volumes:` introduciremos la ruta del archivo `.war` del proyecto. Le asignaremos su puerto debidamente en `ports:` (el 8082:8080) y finalmente en `enviroment:` declararemos el usuario y contraseña del root como en los dos casos anteriores (importante recordar contraseña).

## 3.Pasos para el despliegue de la aplicación

Nos dirigiremos desde la consola al directorio donde se encuentra nuestro docker-compose que en este caso es DOCKER, y introduciremos el comando `sudo docker-compose up` que nos ayuda a construir la imagen, tras lo cual creará y lanzará los contenedores Docker.

![image](https://user-images.githubusercontent.com/91564872/172455258-1d602b8c-9268-4889-969b-765f0011891d.png)

Despues de procesar la construccion de la imagen usaremos el comando `sudo docker ps` para comprobar que todo ha funcionado perfectamente.

![image](https://user-images.githubusercontent.com/91564872/172455527-2d3ecf90-cb9c-4bd9-83c6-4055e30e837b.png)


## 4.Preparación y subida de la imagen a dockerhub.



## 5.Conclusiones
