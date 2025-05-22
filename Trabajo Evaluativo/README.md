# Trabajo Integrador Evaluativo – Reconfiguración de Servicios de Red

## Objetivo

Reconfigurar los servicios DHCP, DNS, HTTP y SSH en un entorno previamente funcional, adaptándolos a nuevos requerimientos de red establecidos por una reorganización empresarial.

---

## Escenario de Evaluación

Estás trabajando como técnico de red en una empresa que ha cambiado su nombre y reorganizado su infraestructura. Como parte del equipo de IT, debés adaptar los servicios ya configurados a las nuevas políticas:

### Cambios requeridos

 # 1. Cambio de Dominio
   - ### Cambiar el dominio actual de `empresa.local` a `nuevaempresa.ar`. **tenes que usar un nombre de dominio que te identifique de forma única**

   - abrimos el archivo de configuracion del dns y cambiamos el nombre a LosPapoticos y le damos una ip de 192.168.4.1(falta actualizar las capturas)


   ![captura 1](./img-dns/Captura%20de%20pantalla%202025-05-21%20113333.png)


   vemos si tiene errores


   ![captura2](./img-dns/Captura%20de%20pantalla%202025-05-21%20113414.png)


   Configuramos la zona inversa


   ![captura3](./img-dns/Captura%20de%20pantalla%202025-05-21%20113435.png)

   (ahi se ve que el dns tiene un 106 cuando tendria que ser un 1 pero al no actualizar las capturas se nos dificulto)


   
   - ### Reconfigurar el servidor **DNS** para reflejar el nuevo dominio.

   Reiniciamos el servidor y verificamos que esté activo


   ![captura4](./img-dns/Captura%20de%20pantalla%202025-05-21%20113516.png)


   Verificamos que funcione mediante un cliente:

   ![captura5](./img-dns/Captura%20de%20pantalla%202025-05-21%20113536.png)


   - ### Asegurar que la resolución de nombres (directa e inversa) funcione correctamente con el nuevo dominio.

   ![captura6](./img-dns/Captura%20de%20pantalla%202025-05-21%20113640.png)

   - ### hacemos ping a la ip del dns

![captura7](./img-dns/Captura%20de%20pantalla%202025-05-21%20214227.png)

   - ### hacemos ping al dns:

![captura8](./img-dns/Captura%20de%20pantalla%202025-05-21%20214300.png)

 # 2. Reconfiguración del DHCP
   - Nuevo rango de direcciones IP: `192.168.x.y - 192.168.x.y`


## Entramos al archivo de configuracion del servidor DHCP:

   - Gateway por defecto: `192.168.x.1`
   - El servidor DNS debe ser el mismo equipo donde está corriendo el servicio DNS.
   - Actualizar el nombre del dominio a `nuevaempresa.ar` /* El nombre de tu eleccion */

![captura1.1](./img-DHCP/Captura%20de%20pantalla%202025-05-21%20113859.png)

   ### - Cambiamos el subnet a 192.168.4.0/24
   ### - Le damos un rando desde la 192.168.4.50 a la 192.168.4.100
   ### - le damos un dominio primario de 192.168.4.1(primario) y 8.8.8.8(secundario)
   ### - Le damos el dns `LosPapoticos.ar`
   ### - definimos el router con la ip 192.168.4.1
   ### - le definimos un broadcast de 192.168.4.255


vemos que el servidor este activo:

![captura2.1](/img-DHCP/Captura%20de%20pantalla%202025-05-21%20113931.png)


   verificamos que se le haya entregado una direccion Ip a un cliente:

![captura3.1](/img-DHCP/Captura%20de%20pantalla%202025-05-21%20114000.png)

Desde una maquina cliente le limpiamos la ip y se la renovamos:


![captura4.1](/img-DHCP/Captura%20de%20pantalla%202025-05-21%20114024.png)

   
 # 3. Servicio HTTP
   - Modificar el contenido de la página principal del sitio web.

   creamos una pagina con el titulo `HOLA VICENTE`

   Luego desde la powershell lo enviamos al directorio /home/luca con el comando scp:


![captura1.3](/img-HTTP/A%20Captura%20de%20pantalla%202025-05-21%20115636.png)


   - El texto debe decir: `Bienvenidos a NuevaEmpresa`.

   (en nuestro caso dice "HOLA VICENTE")

   - Verificamos que el html este en la carpeta:


![captura2.3](/img-HTTP/Captura%20de%20pantalla%202025-05-21%20115538.png)


   - La página debe ser accesible desde un navegador en un cliente de la red mediante: `http://www.nuevaempresa.ar`.

   (en nuestro caso ponemos `http://www.LosPapoticos.ar`)


![captura3.3](/img-HTTP/Captura%20de%20pantalla%202025-05-21%20115706.png)


 # 4. Servicio SSH
   - Cambiar el puerto de escucha de SSH de `22` a `2222`.
   - Configurar para que **sólo el usuario `admin`** pueda iniciar sesión. /* Tambien podes elegir otro usuario */
   - Deshabilitar la autenticación por contraseña.
   - Habilitar el inicio de sesión exclusivamente con claves SSH.


   ![captura1.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20102150.png)


   - Nosotros usamos para este trabajo la powershell de windows la cual ya viene con el protocolo ssh instalado


   - Primero generaremos una llave:


   ![captura2.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20105706.png)


   - vemos si en el directorio .ssh estan las llaves creadas con el comando "ls"


   ![captura3.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20105919.png)


   - Transferimos la clave publica al directorio /home/luca con el comando scp mediante el puerto 2222


   ![captura4.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20110039.png)


   - Por ultimo, ingresamos al usuario desde el puero 2222 como configuramos anteriormente:


   ![captura5.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20110100.png)

---

(Otra opcion)
### Instalamos el PuTTY Key Generator:
- Una vez abierto el programa le damos a generar(MOVER EL CURSOR PARA QUE CARGUE). 
luego de cargar nos dara 2 claves: una publica y una privada


![captura6.4](/img-ssh/Captura%20de%20pantalla%202025-05-21%20112228.png)

tras esto le daremos a la opcion de save public key


tras eso copiaremos el texto que dice ssh-rsa y lo guardaremos


luego en la carpeta ssh crearemos el archivo autorized_keys


![captura7.4](/img-ssh/Captura%20de%20pantalla%202025-05-21%20112330.png)

con el comando chmod 644 le daremos permisos al archivo


luego con el comando nano autorized_keys abrimos el archivo y pegamos la clave


![captura8.4](/img-ssh/Captura%20de%20pantalla%202025-05-21%20112410.png)


(de este proceso desafortunadamente no tenemos captura)


### configurar PuTTY con host, usuario y claves
Es momento de abrir PuTTY y configurar algunas cosas. Al abrirlo, ponemos en la siguiente ventana el host y puerto, que normalmente es el 22:

![captura9.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20205642.png)

Recuerda que el host es el host de tu servidor, o la IP. Ahora vamos a configurar el usuario con el que nos vamos a conectar por defecto, así no tenemos que escribirlo cada vez. Para ello, navegamos a Connection > Data y en Auto-login username escribimos el nombre de usuario de Linux

![captura10.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20210020.png)

Nota: por ejemplo, si pegaste el contenido de la clave pública en el directorio de trabajo de mary (y entonces estabas logueado como mary) entonces pone, de nuevo, mariy para loguearte con ese usuario. Si fuera otro usuario, primero deberías añadirlo a su directorio de trabajo con el proceso de arriba.

Ahora viene el paso más importante, expandimos la sección de SSH, hacemos click en Auth y en donde dice que proporcionemos la clave privada, seleccionamos el archivo de la clave privada haciendo click en Browse (es la que guardamos anteriormente, no es la que copiamos, es la que tiene extensión ppk):

![captura11.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20210250.png)

Nota: aunque en mi caso el espacio a la izquierda de donde dice Browse está vacío, en el tuyo debería tener la ruta de la clave.
Ahora vamos a guardar todo lo que configuramos. Para ello, volvemos a la sección Session y le ponemos un nombre a la misma, luego hacemos click en Save:

![captura12.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20210452.png)

### conectarnos con PuTTY desde Windows a Linux, con SSH
Ahora sí bastará dar doble click en la sesión que guardamos anteriormente (también se puede seleccionar y hacer click en Open)

![captura13.4](./img-ssh/Captura%20de%20pantalla%202025-05-21%20210555.png)

Lo importante es que en la parte de arriba aparece que nos estamos autenticando con el usuario que configuramos en PuTTY, usando la clave privada elegida anteriormente.



---

## Entregables obligatorios

Debés entregar un archivo `.md` por github que contenga:

1. ### Capturas de pantalla
   - Archivo de configuración de `dhcpd.conf` o equivalente.
   - Archivos de zona directa e inversa del DNS.
   - Configuración del servidor web (`index.html` o equivalente).
   - Archivo de configuración `sshd_config`.

2. ### Comprobaciones funcionales
   - Captura de una terminal donde se vea que un cliente obtiene una IP en el nuevo rango.
   - Prueba de resolución del nombre `www.nuevaempresa.ar`.
   - Acceso exitoso al sitio web desde navegador.
   - Acceso por SSH al puerto `2222` usando clave pública (mostrar conexión).

3. ### Informe breve
   - Explicación clara de los pasos realizados.
   - Problemas encontrados (si hubo).
   - Qué aprendiste de la actividad.

---

## Evaluación

- **Total: 10 puntos**
- Se evaluará:
  - Correctitud técnica.
  - Entregables completos.
  - Claridad del informe.
- **Penalización**:
  - Por cada pregunta formulada al docente, se descontarán puntos **dependiendo del nivel de dificultad**.

---