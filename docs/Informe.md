# Práctica de Laboratorio #1

  * Diego Vázquez Campos
  * < alu0101014326@ull.edu.es >, < kaerit@hotmail.com >
  * PE103 - Viernes Oct 16 13:00:00 2020 (UTC +1).
     
# Desarrollo de la práctica

## Preparando el directorio de trabajo general

Como los primeros pasos del informe se abrirá una sesion de trbajo GNU-Linux. En este caso, ya que trabajamos sobre Windows se utilizará el Subsistema Linux de Windows (WSL). El objetivo de la práctica será entrar en contacto con los controladores de versiones. El control de versiones es el registro de los cambios realizados sobre un archivo o conjunto de archivos a lo largo del tiempo, de modo que se puedan recuperar versiones específicas en un momento dado. En este caso, se trabajará con Git.

Git es un software para control de versiones. Su principal caractística es que es distribuido, además, permite el mantenimiento de versiones de aplicaciones cuando éstas tienen un gran número de archivos de código fuente de manera eficiente y fiable.

Lo primero será configurar nuestra información.

```bash
git config --global user.name "Nombre Apellido" 
git config --global user.email "aluXXXXXXXXXX@ull.edu.es"
cat ~/.gitconfig
```

![lpp1.1](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.1.png)

Añadiremos configuraciones más avanzadas. Como por ejemplo, configurar git de manera que no sea necesario introducir la contraseña cada vez que se hace una actualización, otra para que todos los cambios se empujen siempre en el repositorio git, y otra para que se eviten las confirmaciones (commits) innecesarias. Finalmente se ostrará las configuraciones globales. En orden:

```bash
git config --global credential.helper cache
git config --global push.default "matching"
git config --global branch.autosetuprebase always
git config --list
```

![lpp1.2](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.2.png)

## Comenzando con la práctica 1

Se ha de crear la carpeta `mkdir prct01`, y su estrucura de ficheros con sub carpetas `src` y `docs`.

![lpp1.3](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.3.png)

Preparamos el repositorio git y comprobamos que se ha creado la carpeta asociada `.git`.

```bash
git init
```

![lpp1.4](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.4.png)

![lpp1.5](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.5.png)

Antes de realizar una confirmación en un repositorio Git es necesario marcar qué cambios se deben confirmar añadiendo los nuevos ficheros y los ficheros cambiados al `índice del repositorio git`, esto es, al área de preparación. Esto crea una instantánea de los ficheros afectados. Si después de la instantánea, se cambia uno de los ficheros antes de confirmarlos, es necesario añadir el fichero de nuevo al índice para registrar los nuevos cambios. Hay que añadir todos los ficheros y subdirectorios del directorio actual al `índice del repositorio git`. 

![lpp1.6](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.6.png)

```bash
 git log
```

![lpp1.7](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.7.png)

```bash
echo "Hola desde el fichero test01" > test01
echo "Hola desde el fichero test02" > test02
git diff
```

![lpp1.9](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.9.png)


```bash
git commit -a -m "Diciendo hola" 
echo "Adios desde el fichero test01" > test01
echo "Adios desde el fichero test02" > test02
git diff
```

![lpp1.11](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.11.png)

```bash
git add . && git commit -m "Maaaas cambios - con un error sint´actico en el mensaje"
git log
```

![lpp1.10](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.10.png)

Arreglamos el error
```bash
git commit --amend -m "M´as cambios - ahora sin errores"
```

Seguimos haciendo cambios para explotar el alncance de sus funcionalidades, creamos un fichero para luego ver ele fecto de los cambios al borrarlo.
```bash
touch sinsentido.txt
git add . && git commit -m "se ha creado un nuevo fichero sin sentido"
rm sinsentido.txt
git add . && git commit -m "se ha eliminado el fichero sinsentido.txt" 
```

## Usando Github

Como anteriormente ya se disponía una cuenta de Github se ommite el paso del registro y se pasa al momento de comprobar la jerarquía de estructuras con `tree`

```bash
tree
```

![lpp1.12](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.12.png)

Ahora toca proarar la capreta .ssh para generar las claves privada y pública. Haremos una copia de seguridad de las anteriormente generadas para esta práctica. 

```bash
mkdir ~/.ssh/copia
mv ~/.ssh/id_rsa* ~/.ssh/copia/
```

Y ahora generaremos la pareja de claves privada y pública que nos servirá para establecer la conexión segura de cofnianza entre github y nuestra máquina local.

```bash
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub
```

![lpp1.13](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.13.png)

Copiamos el contenido de la clave pública.

![lpp1.14](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.14.png)

La utilizaremos para añadirla a nuestra lista de claves en la cuenta de github y así conceder el acceso desde nuestra máquina a la hora de hacer `push`. 

![](https://i.gyazo.com/dea05f605fe6fa9915aa94af3ccd97aa.png)

Creamos un repositorio vacío en github, sin README ni licencia.

En nuestra máquina crearemos un repositorio remoto con nombre corto ghp01 para referirnos a la jerarquia de carpetas que creamos para prct1, y subir su contenido al repositorio previamente creado en github.


```bash
git remote add ghp01 git@github.com:aluXXXXXXXX/prct01.git 
```

Empujamos el contenido al repositorio y finalmente mostramos detalles de dicho  repositorio remoto

```bash
git push -u ghp01 master
git remote show ghp01 
```

![lpp1.15](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.15.png)

Para mostrar todos los repositorios remotos definidos se utiliza `git remote -v`


## Git e iaaS
El concepto de Infraestructura como Servicio (IaaS, Infrastructure as a Service) es uno de los tres modelos fundamentales en el campo de la computación en la nube (cloud computing), junto con el de Plataforma como Servicio (PaaS, Platform as a Service) y el de Software como Servicio (SaaS, Software as a Service).

Al igual que todos los servicios en la nube, IaaS proporciona acceso a recursos informáticos situados en un entorno virtualizado, la “nube” (cloud), a través de una conexión pública, que suele ser Internet. En el caso de IaaS, los recursos informáticos ofrecidos consisten, en particular, en hardware virtualizado, o, en otras palabras, infraestructura de procesamiento. Físicamente, el repertorio de recursos de hardware disponibles procede de multitud de servidores y redes, generalmente distribuidos entre numerosos centros de datos, de cuyo mantenimiento se encarga el proveedor del servicio en la nube. El cliente, por su parte, obtiene acceso a los componentes virtualizados para construir con ellos su propia plataforma informática. 

Para empezar prepararemos la máquina del Iaas, iniciamos sesión en la máquina creada, tendremos que cambiar el usuario. Allí podemos obtener la IP, para poder conectarnos desde la máquina local vía ssh, también se puede obtener desde la url ( https://iaas.ull.es/mismaquinas ), utilizaremos el mismo procedimiento que hicimos en la máquina local para generar el par de claves privada y pública.

Como la práctica se llevó a cabo en remoto fue necesario utilizar la vpn de la ul cuyo funcionamiento se explica en la propia página.

Configuraremos git de la misma manera que hicimos en pasos previos, copiaremos la clave pública y la añadiremos del mismo modo en github para poder clonar en modo `ssh` el repositorio que actualizamos desde nuestra máquina. 


![](https://i.gyazo.com/90060e4213820fe285a062eef0cf0757.png)

Como podemos ver en la imagen obtenemos el vínculo ssh qu será el que usemos para clonar el repositorio

```bash
 git clone [URL]
```

![lpp1.16](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.16.png)


![lpp1.17](https://github.com/ULL-ESIT-LPP-2021/git-e-iaas-ull-dkaerit/blob/master/assets/LPP.1.17.png)


<i>Guardar los cambios en la copia local, en una confirmación "Modificado nombre".</i>
