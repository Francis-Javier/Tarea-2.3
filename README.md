# Tarea-2.3  

Francisco Javier Díaz Garrón  
21/10/2026  
ASIR 2º  

## 1. Clientes para Oracle Database (en Mint/Debian)  

### 1.1. Cliente gráfico: SQL Developer  

Para esta práctica vamos a instalar, configurar y probar diferentes clientes de conexión (en consola, de escritorio, aplicaciones web y entornos integrados) sobre una máquina cliente Ubuntu para conectarnos a tres Servidores Gestores de Bases de Datos (Oracle, PostgreSQL y MariaDB).  

Para empezar, ejecutamos un `sudo apt update para actualizar la lista de repositorios del sistema y asegurar la descarga de las versiones más recientes.  

![Actualización de repositorios](imagenes/Captura1.png)  

A continuación, ejecutamos sudo apt upgrade para actualizar los paquetes de las instalaciones a sus últimas versiones.  

![Actualizar de paquetes](imagenes/Captura2.png)  

Instalamos los paquetes default-jdk y unzip, necesarios para gestionar los archivos de Java y comprimidos de Oracle.  

![Instalación de Java y Unzip](imagenes/Captura3.png)  

Ejecutando java --version podremos ver la versión de java que tenemos instalada.  

![Observar la versión de Java](imagenes/Captura4.png)  

Accedemos mediante el navegador web a la página oficial de descargas de Oracle SQL Developer para bajar el archivo comprimido .zip, la versión no-jre.  

![Descarga de Oracle SQL Developer](imagenes/Captura5.png)  

Descomprimimos el archivo descargado en el directorio /opt/ mediante el comando sudo unzip.  

![Descomprimir SQL Developer en /opt](imagenes/Captura6.png)  

Al intentar ejecutar SQL Developer por primera vez mediante ./sqldeveloper.sh, el sistema nos devuelve un error debido a que requiere JDK 17 o superior y el sistema está usando la versión 11.  

![Error de versión de JDK en SQL Developer](imagenes/Captura7.png)  

Solucionamos el problema instalando la versión OpenJDK 17 con el comando sudo apt install openjdk-17-jdk -y.  

![Instalación de OpenJDK 17](imagenes/Captura8.png)  

Ahora con sudo update-alternatives --config java podemos ver la opción predefinida de java que tiene el sistema, en mi caso al instalar la versión 17 se a puesto automaticamente la primera, pero si no tendria que cambiarse para que fuera la primera.  

![Opciones de java en update-alternatives](imagenes/Captura9.png)  

Comprobamos de nuevo con java --version que la versión activa ahora es OpenJDK 17.0.20.1.  

![Verificación de Java 17](imagenes/Captura10.png)  

Creamos el acceso directo para el menú de aplicaciones del sistema en /usr/share/applications/sqldeveloper.desktop utilizando sudo tee.  

![Creación del acceso directo de sql](imagenes/Captura11.png)  

Abrimos SQL Developer, y ahora vamos a añadir una conexión, para eso hacemos clic en la cruz verde de la izquierda arriba, y luego ponemos los datos de la conexión, como un nombre identificativo de la conexión, el puerto por donde pasara la información, el nombre de usuario y su contraseña, el nombre de la base de datos en Nombre del servicio, y la IP del servidor donde esta el gestor.  

![Configuración de la conexión en SQL Developer](imagenes/Captura14.png)  

Y al darle a conectar no vemos ningun error, y en la columna de la izquierda vemos el nombre que le pusimos a la conexión hace un momento, entonces la conexión a sido un exito y ya estamos conectados a la base de datos.  

![Comprobación de conexión en SQL Developer](imagenes/Captura15.png)  

### 1.2. Cliente gráfico: VS Code y extensión SQL Developer  

Para este cliente necesitamos Visual Studio Code, si no lo tenemos instalado, tenemos que ir al navegador y acceder a la página oficial de VS Code, y descargar el paquete .deb  

![Descarga de VS Code](imagenes/Captura12.png)  

Instalamos el paquete descargado en la terminal con sudo apt install ./code_1.142.0-1792035033_amd64.deb.  

![Instalación de VS Code](imagenes/Captura13.png)  

Abrimos VS Code, buscamos en Extensiones **Oracle SQL Developer for VS Code** y hacemos clic en instalar.  

![Instalación de extensión Oracle en VS Code](imagenes/Captura16.png)  

Accedemos a la pantalla de bienvenida de la extensión de Oracle dentro de VS Code, haciendo clic en el último icono de la columna de la izquierda, el nuevo que se a añadido.  

![Pantalla de inicio de la extensión Oracle](imagenes/Captura17.png)  

Ahora tenemos que configurar la conexión, para eso necesitamos ponerle un nombre identificativo a la conexión, indicarle la IP del servidor, el puerto por donde pasara la información, el nombre de la base de datos, el nombre de usuario y su contraseña, con esos datos ya si podriamos tener una conexión sin problemas.  

![Configuración de conexión en VS Code](imagenes/Captura18.png)  

Y si todo a ido bien deberíamos poder ver a la izquierda una columna con el nombre que le pusimos a la conexión con la base de datos, mostrando las tablas, vistas, etc....  

![Comprobación de conexión](imagenes/Captura19.png)  

### 1.3. Cliente de terminal: SQL*Plus  

Accedemos a la web de Oracle para descargar los paquetes de Oracle Instant Client.  

![Descarga de Oracle Instant Client](imagenes/Captura20.png)  

Seleccionamos la descarga del archivo comprimido del paquete básico `instantclient-basic-linux.x64-23.26.3.0.0.zip`.  

![Descarga de Instant Client Basic](imagenes/Captura21.png)  

Descargamos también el paquete complementario de línea de comandos `instantclient-sqlplus-linux.x64-23.26.3.0.0.zip`.  

![Descarga del paquete SQL*Plus](imagenes/Captura22.png)  

Creamos el directorio de destino en nuestra carpeta personal usando mkdir -p ~/oracle-client.  

![Creación de directorio oracle-client](imagenes/Captura23.png)  

Descomprimimos el paquete básico de Instant Client dentro del directorio creado.  

![Descompresión de Instant Client Basic](imagenes/Captura24.png)  

Descomprimimos el paquete de SQL*Plus en la misma ubicación.  

![Descompresión de SQL*Plus](imagenes/Captura25.png)  

Comprobamos con ls ~/oracle-client/ que los archivos del cliente se han descomprimido correctamente.  

![Verificación de ficheros de Instant Client](imagenes/Captura26.png)  

Exportamos las variables de entorno LD_LIBRARY_PATH y PATH para la sesión actual e intentamos ejecutar sqlplus -v, obteniendo un error porque nos falta la librería libaio.so.1.  

![Error de falta de librería libaio](imagenes/Captura27.png)  

Para arreglar el error que nos a dado simplemente descargamos la libreria que nos hace falta con sudo apt update && sudo apt install libaio1.  

![Instalación de libaio1](imagenes/Captura28.png)  

Ejecutando sqlplus -v podremos ver la versión de SQL*Plus que tenemos instalada, y que ya no da error.  

![Observar la versión de SQL*Plus](imagenes/Captura29.png)  

Nos conectamos a la base de datos remota de Oracle usando el comando sqlplus orauser@//IP DEL SERVIDOR:1521/FREEPDB1.  

![Conexión por consola con SQL*Plus](imagenes/Captura30.png)  

### 1.4. Cliente de terminal: SQLcl  

Entramos en la página oficial para descargar la herramienta Oracle SQLcl.  

![Página de descarga de SQLcl](imagenes/Captura31.png)  

Descomprimimos el paquete comprimido descargado usando unzip ./sqlcl-latest.zip -d ~/sqlcl.  

![Descompresión de SQLcl](imagenes/Captura32.png)  

Ejecutando ~/sqlcl/sqlcl/bin/sql -version podremos ver la versión de SQLcl que tenemos instalada.  

![Observar la la versión de SQLcl](imagenes/Captura33.png)  

Añadimos la ruta del binario de SQLcl a nuestro archivo de configuración personal ~/.bashrc para poder ejecutarlo desde cualquier directorio.  

![Configuración del PATH para SQLcl](imagenes/Captura34.png)  

Recargamos la configuración de entorno con source ~/.bashrc y nos conectamos con el comando sql orauser@//IP del servidor:1521/FREEPDB1.  

![Conexión exitosa con SQLcl](imagenes/Captura35.png)  

## 2. Clientes para PostgreSQL  

### 2.1. Cliente de terminal: psql  

Actualizamos los repositorios antes de comenzar la instalación de los componentes de PostgreSQL.  

![Actualizar lista de paquetes](imagenes/Captura36.png)  

Instalamos la herramienta de línea de comandos de PostgreSQL mediante sudo apt install postgresql-client.  

![Instalación del cliente de PostgreSQL](imagenes/Captura37.png)  

Ejecutamos psql --version para poder ver que versión de psql tenemos instalada.  

![Observar la versión de psql](imagenes/Captura38.png)  

Nos conectamos a la base de datos remota de PostgreSQL usando psql -h IP de la maquina del servidor -U pguser -d dbpg -W.  

![Conexión remota con psql](imagenes/Captura39.png)  

### 2.2. Cliente gráfico: pgAdmin 4  

Consultamos la documentación oficial para saber si nuestra versión de Ubuntu es compatible con pgAdmin.  

![Página oficial de instalación de pgAdmin 4](imagenes/Captura40.png)  

Instalamos los paquetes auxiliares curl, gnupg y lsb-release para gestionar las claves de firma y repositorios.  

![Instalación de paquetes requeridos](imagenes/Captura41.png)  

Descargamos e importamos la clave GPG pública del repositorio de pgAdmin 4.  

![Importación de la clave GPG](imagenes/Captura42.png)  

Añadimos el archivo de repositorio oficial en /etc/apt/sources.list.d/pgadmin4.list.  

![Añadir repositorio APT de pgAdmin](imagenes/Captura43.png)  

Actualizamos el sistema con sudo apt update para incluir la lista de paquetes del nuevo repositorio de pgAdmin.  

![Actualización de repositorios con pgAdmin](imagenes/Captura44.png)  

Instalamos la aplicación de escritorio de pgAdmin ejecutando sudo apt install pgadmin4-desktop.  

![Instalación del paquete pgadmin4-desktop](imagenes/Captura45.png)  

Iniciamos la aplicación gráfica pgAdmin 4 y observamos la pantalla principal de bienvenida.  

![Pantalla principal de pgAdmin 4](imagenes/Captura46.png)  

Ahora vamos a establecer comunicación con el servidor, esa comunicación debe tener un nombre por lo que ponemos uno que identifique la conexión  

![Nombre de la conexión en pgAdmin](imagenes/Captura47.png)  

Y ahora lo que tendremos que hacer es poner los datos de la conexión con el servidor que tiene el gestor de la base de datos, para eso indicamos la IP del servidor, el nombre de usuario, contraseña, el nombre de la base de datos y el puerto por donde pasara la conexión.  

![Datos de la conexión en pgAdmin](imagenes/Captura48.png)  

Y ya como podemos ver en la captura en la columna de la izquierda aparece que estamos conectados a un servidor, y por ese motivo la conexión a sido un exito.  

![Comprobación del cliente pgAdmin](imagenes/Captura49.png)  

## 3. Clientes para MariaDB  

### 3.1. Cliente de terminal: mariadb (o mysql)  

Antes de instalar los clientes hacemos un sudo apt update para actualizar los paquetes de la terminal..  

![Actualizar terminal](imagenes/Captura50.png)  

Instalamos el cliente nativo de MariaDB con sudo apt install mariadb-client.  

![Instalación del cliente MariaDB](imagenes/Captura51.png)  

Ejecutamos mariadb --version para ver la versión del cliente que tenemos.  

![Comprobación de la versión de MariaDB](imagenes/Captura52.png)  

Nos conectamos por línea de comandos al servidor remoto de MariaDB con el comando mariadb -h IP DEL SERVIDOR -u muser -p dbm.  

![Conexión con cliente a MariaDB](imagenes/Captura53.png)  

### 3.2. Cliente web: phpMyAdmin  

Instalamos el servidor Apache, el soporte para PHP y el paquete de phpMyAdmin ejecutando sudo apt install apache2 php php-mysql php-mbstring php-zip php-gd php-curl phpmyadmin.  

![Instalación de Apache, PHP y phpMyAdmin](imagenes/Captura54.png)  

Durante el asistente interactivo de instalación, seleccionamos `apache2` como el servidor web a reconfigurar automáticamente.  

![Selección de Apache en el asistente](imagenes/Captura55.png)  

Seleccionamos Sí cuando la instalación pregunta si deseamos configurar la base de datos con dbconfig-common.  

![Configuración dbconfig-common](imagenes/Captura56.png)  

Establecemos la contraseña de aplicación MySQL/MariaDB para phpMyAdmin, esta contraseña solo la usaremos con el instalador.  

![Introducción de contraseña](imagenes/Captura57.png)  

Confirmamos de nuevo la contraseña introducida.  

![Confirmación de contraseña](imagenes/Captura58.png)  

El instalador muestra un aviso de error al no detectar un servidor MySQL local escuchando en el socket `/run/mysqld/mysqld.sock`, por ahora ignoramos el aviso de error.  

![Aviso de error de socket local](imagenes/Captura59.png)  

Seleccionamos la opción `ignorar` en el menú del instalador para continuar, y seguir con la instalación, y luego arreglaremos ese error.  

![Opción ignorar error en el instalador](imagenes/Captura60.png)  

Para arreglar el error que nos a dado tenemos que hacer nano al archivo de configuración de phpMyAdmin que es el que se ve en la captura, y cambiar el host por la IP donde se encuentra el gestor, ya que si no solo se conectara con nuestro equipo, y al ser cliente no tiene la base de datos por lo que da error, y aparte tambien tendremos que descomenter algunas lineas.  
![Entrar al archivo de phpMyAdmin](imagenes/Captura61.png)  

Ahora lo que tendremos que hacer será descomentar las lineas que aparecen en la captura, las que no son azules, quitando las //, y en la linea donde aparece host, escribir la dirección IP de la máquina donde esta el gestor de base de datos, ya que sino solo se intentara conectar con nuestro equipo y como es un cliente no tiene base de datos por lo que dará error si no lo indicamos.  

![configuración del archivo de phpMyAdmin](imagenes/Captura62.png)  

Y para que toda la nueva información que hemos indicado sea activa, tendremos que ejecutar un sudo systemctl restart apache2, para actualizar la información.  

![reinicio del servicio de apache2](imagenes/Captura63.png)  

Ahora tendremos que entrar en el navegador y escribir  http://localhost/phpmyadmin/, para acceder a la página de inicio de phpMyAdmin, aquí tendremos únicamente que escribir el nombre de usuario, contraseña, y la dirección del servidor al que queremos establecer conexión.  

![Login de phpMyAdmin](imagenes/Captura64.png)  

Y si no nos a dado ningún error al conectarnos, ya nos habremos establecido una conexión con la base de datos, como se muestra en la imagen.  

![Comprobación de conexión con la base de datos con PHPMyAdmin](imagenes/Captura65.png)  

## 4. Clientes para varios SGBD  

### 4.1. DBeaver Community  

Ahora vamos a descargar un cliente de base de datos el cual sirve para varios gestores, el primero será DBeaver, después adminer, para eso nos vamos a la página oficial y lo descargamos.  

![Descargar DBeaver](imagenes/Captura66.png)  

Ahora que ya nos hemos descargado el paquete desde la página oficial, lo que hay que hacer es instalarlo en la máquina por lo que nos posicionamos en la carpeta de Descargas y ejecutamosd, sudo apt install ./NOMBRE_DEL_ARCHIVO_DBEAVER.deb para instalarlo.  

![Instalar el paquete de DBeaver](imagenes/Captura67.png)  

Ahora que ya estamos en la aplicación gráfica de DBeaver lo que debemos hacer es entamblar una conexión con un gestor de base de datos, para eso hacemos clic en el icono de un cable con un + en la parte superior izquierda.  

![Iniciar una conexión en DBeaver](imagenes/Captura68.png)  

Ya estando en el asistente, aparecerán muchos gestores con los que podemos establecer conexión, en este caso será con PostgreSQL, por lo que elegimos la opción de PostgreSQL.  

![Selección de conexión con PostgreSQL](imagenes/Captura69.png)  

Ahora que ya hemos seleccionado una conexión con PostgreSQL, lo que tenemos que hacer es indicar los datos de esa conexión, como la IP de la máquina donde se encuentra el gestor de la base de datos, el puerto por donde pasara la información, el nombre de la base de datos, el nombre del usuario y su contraseña.  

![Datos de la conexión de PostgreSQL](imagenes/Captura70.png)  

Lo siguiente es descargar los drivers, para que pueda funcionar la conexión y no haya problemas.  

![Descargar drivers de PostgreSQL](imagenes/Captura71.png)  

Y si ahora vemos la columna de la izquierda podemos ver que aparece el nombre de la base de datos, por lo que la conexión a sido un exito.  

![Comprobación de conexión con PostgreSQL](imagenes/Captura72.png)  

Ahora volvemos al asistente y esta vez seleccionamos MariaDB, para conectarnos a la base de datos de MariaDB.  

![Selección de conexión con MariaDB](imagenes/Captura73.png)  

Y ahora tenemos que aportar los datos de la conexión con el gestor de MariaDB, para eso debemos indicar la IP donde se encuentra el gestor de la base de datos, el puerto por donde va a ir la comunicación, el nombre de la base de datos, el nombre de usuario y su contraseña.  

![Datos de la conexión con MariaDB](imagenes/Captura74.png)  

Lo último que tendremos que hacer antes de ya conectarnos es descargar los drivers para poder conectarnos sin problemas.  

![Descargar drivers de MariaDB](imagenes/Captura75.png)  

Y si todo a ido bien deberiamos poder ver lo que aparece en la captura, el cual podemos ver que en la columna de la izquierda ya nos aparece la base de datos de MariaDB.  

![Comprobación de conexión con MariaDB](imagenes/Captura76.png)  

Y para acabar vamos a elegir Oracle para poder conectarnos a la base de datos con DBeaver.  

![Selección de conexión con Oracle](imagenes/Captura77.png)  

Y ahora lo que tendremos que hacer, al igual que hicimos con mariadb y postgreSQL es rellenar los datos de la conexión con Oracle, indicando la IP del servidor donde esta el gestor, el puerto, el nombre de la base de datos, nombre de usuario y contraseña.  

![Datos de la conexión con oracle](imagenes/Captura78.png)  

Despues debemos descargar el driver de oracle para que pueda funcionar la configuración.  

![Descargar driver de oracle](imagenes/Captura79.png)  

Y ya podemos ver que como paso con mariadb y postgreSQL, ya estamos conectados con oracle y podemos configurar la base de datos.  

![Comprobación de oracle](imagenes/Captura80.png)  

### 4.2. Adminer  

Lo primero que hace falta para usar adminer, el cual es un archivo PHP, es instalar la interfaz CLI con sudo apt install php-cli  

![Instalar interfaz de adminer](imagenes/Captura81.png)  

Lo siguiente que debemos hacer es descargar el archivo ejecutable de adminer desde su pagina oficial, para eso ejecutamos wget https://www.adminer.org/latest.php -O adminer.php  

![Descargar el archivo ejecutable de adminer](imagenes/Captura82.png)  

Y lo unico que debemos hacer ahora es usar php -S 127.0.0.1:8080 adminer.php, para iniciar el servidor y que podamos usar el cliente de base de datos.  

![Iniciar el servidor de adminer](imagenes/Captura83.png)  

Después de haber iniciado el servidor, tenemos que ir al navegador y escribir http://localhost:8080, para acceder al cliente adminer, y estaremos en el login de adminer, por lo que ahora tendremos que elegir que gestor de base de datos nos vamos a conectar, en mi caso MariaDB, por lo que solo hay que escribir la IP del servidor donde se encuentra el gestor, el usuario contraseña y nombre de la base de datos.  

![Pantalla de login de adminer](imagenes/Captura84.png)  

Y si todo a ido bien deberíamos ver lo que aparece en esta captura de pantalla, y es que esto es la pantalla de inicio de adminer, por lo que hemos entrado sin problemas y podemos trabajar con la base de datos de mariadb.  

![Pantalla de inicio de Adminer](imagenes/Captura85.png)  

Y para acabar lo último que vamos a hacer es pulsar control mas c para cerrar el servidor y acabar la práctica.  

![Cerrar el cliente](imagenes/Captura86.png)  
