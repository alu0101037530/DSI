# DSI
Tras realizar los pasos del primer inicio de sesion y cambio de clave obligatorio en el iaas, comenzamos los pasos para poder conectarnos desde la terminal de nuestro ordenador, ya que el teclado del iaas apenas es funcional.
En primer lugar debemos conocer la direccion ip de la maquina a la que nos conectaremos. En mi caso es:

usuario@ubuntu:~$ ifconfig
ens3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.6.128.48  netmask 255.255.254.0  broadcast 10.6.129.255
        inet6 fe80::21a:4aff:fe97:532b  prefixlen 64  scopeid 0x20<link>
        ether 00:1a:4a:97:53:2b  txqueuelen 1000  (Ethernet)
        RX packets 84564  bytes 40100549 (40.1 MB)
        RX errors 0  dropped 42  overruns 0  frame 0
        TX packets 8530  bytes 980794 (980.7 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
Generamos una clave -trsa con el nombre del archivo donde guardaremos la clave pero ,en este caso, sin contraseña.
Una vez realizado esto, creamos un fichero config en la direccion .ssh donde incluiremos un nombre de host para conectarnos y la direccion ip de la maquina en cuestio.

jordi@jordi-X550VX:~$ cat ~/.ssh/config 
Host dsi
HostName 10.6.128.48
user usuario
IdentityFile /Users/alu0101037530/.ssh/miclave
ServerAliveInterval 240

El paso siguiente sera añadir en la maquina, los contenidos de miclave.pub en un fichero de claves autorizadas:

usuario@ubuntu:~$ cat .ssh/authorized_keys 
ssh-rsa AAAAB3NzaDfrXUayyp2dXOyxmdU65LhxX4VEcQFa8Yn+kmBnbIuSbcya1thLhorq8SzweFk/1/WO/SIBO1o8MG79osnAIn9xTc43Q2Od9VvnN2Gwex3MIyGy+2TUZ4ge9ma1E8oKfD5bgESnaYUXC55oB5Riugt6u5h6Joq+7EXHGGm6cuq999OxTH0BA8xCyC2I43TfBByMPhZnbYlh6pEtsSrI11v jordi@jordi-X550VX

Una vez realizados estos pasos ya deberiamos poder conectarnos desde la terminal de nuestro ordenador, facilitando asi el resto de pasos que nos quedan.
Instalaciones:
1º debemos intalar git, en caso de que no este instalado. En mi caso no fue necesaria la instalacion.

usuario@ubuntu:~$ git --version
git version 2.17.1

Comprobamos de igual manera si nodejs se encuentra instalado.

usuario@ubuntu:~$ nodejs --version
v8.10.0

Realizamos un enlace simbolico entre node.js y node una vez comprobamos que poseemos node.

usuario@ubuntu:~$ node --version
v11.9.0

Podemos observar que se ha realizado con exito ya que no no sale falla a la hora de solicitar la version de node.
Procedemos a la instalacion de nvm y su correspondiente actualizacion, obteniendo la siguiente lista.

usuario@ubuntu:~$ nvm list
->      v11.9.0
         system
default -> node (-> v11.9.0)
node -> stable (-> v11.9.0) (default)
stable -> 11.9 (-> v11.9.0) (default)
iojs -> N/A (default)
lts/* -> lts/dubnium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.16.0 (-> N/A)
lts/carbon -> v8.15.0 (-> N/A)
lts/dubnium -> v10.15.1 (-> N/A)

Configurar el cliente ssh para trabajar con GitHub:
Para poder trabajar con Github debemos crear la correspondiente clave y que nos permita asi, trabajar con él. Destacar en este punto el problema sufrido a la hora de intentar hacer la clave con -tdsa en lugar de -trsa.
En el caso de -tdsa no me permitia acceder dandome un error correspondiente a un permiso denegado de acceso en la clave publica de github, por lo tanto opte por crear otra clave con trsa y copiarla en la pagina de github.
Creamos un fichero config en la maquina siguiendo los pasos que hicimos para poder acceder a la maquina desde la terminal, pero la finalidad de esta ocasion es acceder a github desde la terminal.
El fichero config nos queda tal que asi:

usuario@ubuntu:~$ cat ~/.ssh/config
Host github.com
Hostname github.com
user git
IdentityFile /home/usuario/.ssh/miclaveparagithub
 Sabre
Creamos unos directorios donde clonar github, y una vez creados procedemos a clonarlo. Sabremos que ha funcionado cuando veamos la carpeta de lo que hemos clonado en el directorio corespondiente.

usuario@ubuntu:~$ cd src/sytw/
usuario@ubuntu:~/src/sytw$ ls
express-start

Como ya sabemos que se ha creado con exito, entramos en la carpeta Hello perteneciente al repositorio y localizamos la direccion ip del ejemplo donde se esta escuchando la app.
La introducimos en la terminal y obtenemos el siguiente resultado:


Solo nos quedaria hacer logout de la maquina.
