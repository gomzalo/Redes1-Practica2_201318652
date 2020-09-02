# MANUAL DE CONFIGURACIÓN
## Requisitos

* **GNS3**
Para esta practica se utilizará la versión 2.2.11.
![AcercaDeGNS.png](https://www.dropbox.com/s/ywpvuz7fudo65n5/AcercaDeGNS.png?dl=0&raw=1)

* **Imagen Router**
Debemos descargar la [imagen](https://ingenieriausacedu-my.sharepoint.com/:u:/g/personal/3003608000101_ingenieria_usac_edu_gt/Edt3tNlwlx5PrK4hHTVCpBwBdBbYaRe2zexDQJB4wg0Y2Q?e=Vsh7Ad) del router que utilizaremos en la practica, pues GNS3 no la trae.
![Router.png](https://www.dropbox.com/s/cjg84l62b4o3rru/Router.png?dl=0&raw=1)

* **ISO Tiny Core Linux**
También usaremos una máquina virtual para simular una fisica, en este caso utilizaremos [Tiny Core Linux](http://tinycorelinux.net/11.x/x86/release/CorePlus-current.iso). (en su ultima versión)
![TinyL.png](https://liliputing-wpengine.netdna-ssl.com/wp-content/uploads/2017/04/tinycore.jpg)

### Creación del proyecto

Creamos el proyecto en GNS3, nuestro proyecto se llamara Redes1-Practica2_201318652.

![creando_proyecto.png](https://www.dropbox.com/s/ne5vb82p9k18hvq/creando_proyecto.png?dl=0&raw=1)

## Diseño
 
Al crear el proyecto se nos muestra un espacio en blanco, como se ve en la imagen. 
 ![creacion.png](https://www.dropbox.com/s/klqkrccmuthhwsz/creacion.png?dl=0&raw=1)
Se debe de presionar el menu lateral izquierdo donde se encuentran los diferentes equipos que utilizaremos para nuestra topologia.

#### Infraestructura

Nuestra infraestructura estara compuesta por los siguientes elementos:
- 1 Router
- 3 Switches
- 6 Maquinas host (cliente)
    -  5 VPCs
    -  1 Virtual

#### Topología

##### Red
Se configurara una topologia para una empresa, la cual tiene 6 mauinas distribuidas de la siguiente manera:

| Departamento | Cantidad de Host |
|--------------|------------------|
| Finanzas     | 2                |
| Ventas       | 3                | 
| Informática  | 1                | 

Cada una de estas tendrá su propia subred para poder llevar una mejor gestión y control
de cada departamento, pero también se necesitan que todas puedan comunicarse entre
sí por medio de 1 router.

##### Subredes
La dirección de red proporcionada es la 192.168.1**X**.0/24 la cual administra distintas
subredes. Estas subredes ya están definidas a continuación:
![subredes.png](https://www.dropbox.com/s/tnpftp1p72rle48/subredes.png?dl=0&raw=1)
Se asignan direcciones válidas dentro de cada rango de direcciones asignables
para los hosts pertenecientes a la red, llenando la siguiente tabla.
![subredes_ipasignada.png](https://www.dropbox.com/s/pdtb1pkxjfm33ui/subredes_ipasignada.png?dl=0&raw=1)

Nota: La X representa el 4to número del carné de derecha a izquierda. Ejemplo:
200012345
• PC1: 192.168.12.22/26 192.168.12.1
• PC2: 192.168.12.32/26 192.168.12.1

Respecto a la nota anterior, el carné es 20131**8**652, por lo tanto el valor de X será:
* X = 8

Aplicando dichos valores a las IPs que se usaran, quedarian de la siguiente forma:

| Dirección de red      | Primera dirección asignable | Última dirección asignable | Dirección de Broadcast |
|-----------------------|-----------------------------|----------------------------|------------------------|
| **192.168.18.0/24**   | 192.168.18.1                | 192.168.18.62              | 192.168.18.63          |
| **192.168.18.64/24**  | 192.168.18.65               | 192.168.18.126             | 192.168.18.127         |
| **192.168.18.128/24** | 192.168.18.129              | 192.168.18.190             | 192.168.18.191         |

Y las direcciones validas serán las siguientes.

| Dispositivo 	| Dirección IP 	| Máscara de red  	| Gateway        	|
|-------------	|--------------	|-----------------	|----------------	|
| **PC1**     	|              	| 255.255.255.192 	| 192.168.18.1   	|
| **PC2**     	|              	| 255.255.255.192 	| 192.168.18.1   	|
| **PC3**     	|              	| 255.255.255.192 	| 192.168.18.65  	|
| **PC4**     	|              	| 255.255.255.192 	| 192.168.18.65  	|
| **PC5**     	|              	| 255.255.255.192 	| 192.168.18.65  	|
| **PC6**     	|              	| 255.255.255.192 	| 192.168.18.129 	|

##### Diagrama

La topología queda como se ve en la siguiente imagen.

![topologiap2.png](https://www.dropbox.com/s/zhwaawejko1lnqb/topologiap2.png?dl=0&raw=1)

### Conexión

* SW1, SW2 y SW3 se conectan al router.
* VPC1 y VPC2 se conecta a SW1.
* VPC3, VPC4 y VPC5 se conectan a SW2.
* Virtual se conecta a SW3.

## Asignación de IPs

Luego de haber finalizado con la conexión y el etiquetado de las IPs correspondientes a cada nodo en la topología, se procedera a asignar estas a cada equipo y a *levantar* los equipos.

##### Router
El principal nodo, conector de nuestra red, contiene dos interfaces, cada una conectada a un switch.
Para configurar este dispositivo, y sus interfaces, debemos seguir los siguientes pasos.

1. Iniciar el dispositivo
![IniciarRouter.png](https://www.dropbox.com/s/gva3wqxcohc3d49/IniciarRouter.png?dl=0&raw=1)0

    *   Una vez el dispositivo este *corriendo*, se cambiara el color de la conexión a verde.
    ![RouterCorriendo.png](https://www.dropbox.com/s/j4clbftt7x4k13l/RouterCorriendo.png?dl=0&raw=1)

2. Configurar el dispositivo
Ahora toca asignar la ip, daremos click derecho sobre el router y seleccionaremos la opción que dice *Console*, para acceder a la consola que nos permitira ejecutar los comandos necesarios para llevar a cabo esta acción.
![RouterConsole.png](https://www.dropbox.com/s/9jx0792h31z3l61/RouterConsole.png?dl=0&raw=1)
    * Se nos abrira una sesión en consola de Putty, como se puede observar.
    ![RouterPutty.png](https://www.dropbox.com/s/tj6zs1guthjkdjz/RouterPutty.png?dl=0&raw=1)
    * Presionamos enter, para poder iniciar la configuración. A continuación, usaremos el siguiente comando para ver el estado de las interfaces.
        ```sh
        $ sh ip int brief
        ```
        ![Routershipintbrief.png](https://www.dropbox.com/s/4w7u79c8unw5455/Routershipintbrief.png?dl=0&raw=1)
        Al no haber configurado ninguna, nos aparecera como la imagen superior.
        
    * Escribiremos el siguiente comando para inciar la configuración de las interfaces

        ```sh
        $ conf t
        ```

    * Empezamos por configurar la interfaz FastEthernet0/0, con el siguiente comando:
        ```sh
        $ int f0/0
        ```
        ![RouterConfIntF0.png](https://www.dropbox.com/s/jbb0vekihopfdfx/RouterConfIntF0.png?dl=0&raw=1)

    * El siguiente comando nos servira para asignar la IP a la interfaz.
    
        ```sh
        $ ip address <IP> <Mascara de red>
        ```
        En nuestro caso, seria la siguiente:
        ```sh
        $ ip address 192.168.18.1 255.255.255.192
        ```
    * Luego de esto, activaremos la interfaz con el siguiente comando:
        ```sh
        $ no shut
        ```
         Con esto ya quedo, nuestra interfaz configurada. Ahora vamos a volver al *menu principal* debemos usar el siguiente comando 2 veces. Una para salir de la interfaz y otro para salir del menu configuración.

        ```sh
        $ exit
        ```
    * ¨Para guardar los cambios realizados en el router, se utiliza el siguiente comando.
    
        ```sh
        $ wr
        ```
    
     **La configuración para la interfaz f0/1, es exactamente los mismos pasos con la diferencia de que su IP sera la 192.168.18.65, mientras que para la interfaz f1/0 la IP es 192.168.18.129**
     
     *  Por ultimo, se verifica el estado de las interfaces. Se puede observar que los cambios han sido guardados y aplicados correctamente.
    ![shipintbrr1.png](https://www.dropbox.com/s/wm308igo0ybiagc/shipintbrr1.png?dl=0&raw=1)
    
##### Switches
Estos dispositivos al no guardar mayor información, su función en esta topología es replicar las conexiones entrantes. No necesita configuración alguna.
Esto quiere decir, que dependiendo a la interfaz a la que se conecten esas seran las IPs que regiran las maquinas que se conecten a estos.

| ![SW1p2.png](https://www.dropbox.com/s/dddjxlm4m8fcl3p/SW1p2.png?dl=0&raw=1) 	| ![SW2p2.png](https://www.dropbox.com/s/ydszquebyh23bws/SW2p2.png?dl=0&raw=1) 	| ![SW3.png](https://www.dropbox.com/s/4ijz339fdxhqdin/SW3.png?dl=0&raw=1) 	|
|------------------------------------------------------------------------------	|------------------------------------------------------------------------------	|--------------------------------------------------------------------------	|

##### VPCs
Estos dispositivos emulan una maquina, solamente corriendo en consola (por ahorro de recursos).
Para su configuración se deben seguir los siguientes pasos:

1. Iniciar el dispositivo
Al igual que con el router, al hacerlo la conexión se tornara verde.
![VPCIniciar.png](https://www.dropbox.com/s/xn5c5q0fjl4im8p/VPCIniciar.png?dl=0&raw=1)
2. Configurar el dispositivo
Para asignar la ip de este dispositivo, de igual forma, se presiona click derecho y se selecciona la opción *Console*.
![VPCConsole.png](https://www.dropbox.com/s/si4sdgl6bu00rip/VPCConsole.png?dl=0&raw=1)
    * Al hacer esto se nos abrira una consola, mostrando la IP que tiene asignada actualmente la VPC.
    ![VPCMenuConsole.png](https://www.dropbox.com/s/kjvzc3av5oy188c/VPCMenuConsole.png?dl=0&raw=1)
    (En la imagen ya se le asigno la IP requerida para esta practica a la VPC1)
    * Para asignar la IP se debe usar el siguiente comando:
        ```sh
        $ ip <IP>/<Tamaño mascara> <IP Mascara>
        ```
      En nuestro caso, seria la siguiente:
        ```sh
        $ ip 192.168.18.2/26 192.168.18.1
        ```
    * Para guardar los cambios en la VPC se usa el siguiente comando:
        ```sh
        $ save
        ```
        ![VPCSave.png](https://www.dropbox.com/s/vshppmzstgrdx9p/VPCSave.png?dl=0&raw=1)
    * Por ultimo para ver el estado de la IP, se usara el siguiente comando. Como se puede observar, se ha aplicado y guardado correctamente la IP que se requiria.
        ```sh
        $ sh ip
        ```
        
        ![shipvpc1p2.png](https://www.dropbox.com/s/ousgo61gro9ym69/shipvpc1p2.png?dl=0&raw=1)
        
         **La configuración para las VPC2, VPC3, VPC4 y VPC5 es exactamente los mismos pasos con la diferencia de que sus direcciones deberan respetar los rangos de sus subredes respectivamente**
         
##### Linux Virtual
Para la configuración de la IP de esta maquina virtual, se utiliza VMWare Workstation como programa para *levantar* dicha maquina.
* Dando por hecho que la instalación de la maquina ya se ha realizado, hay una configuración extra que debe hacerse para que funcione dicha maquina.
    *  **VMWare**
        1. Ir al menu *edit* y seleccionar la opción *Virtual Network Editor...*
        ![EditVMW.png](https://www.dropbox.com/s/skne2lx7s9e9rrg/EditVMW.png?dl=0&raw=1)
        2. A continuación se mostrara una ventana, elegir la opción *Add a New Network*, como host only.
        ![VMWAddNet.png](https://www.dropbox.com/s/cfa1lm3cnwiowpj/VMWAddNet.png?dl=0&raw=1)
        3. En la configuración de la red que usara la maquina virtual debemos elegir la nueva red virtual recién creada.
        ![VMSett.png](https://www.dropbox.com/s/jh87uvihwwuuml4/VMSett.png?dl=0&raw=1)
    * **GNS3**
        1. Ir al menu *edit* y seleccionar la opción *prefferences*.
        ![GNSedit.png](https://www.dropbox.com/s/uvzifj0mpekt0bk/GNSedit.png?dl=0&raw=1)
        2. En el menu izquierdo, seleccionar *VMware* y en la pestaña *Advanced local settings* presionar *configure*.
        ![GNSVMConf.png](https://www.dropbox.com/s/pkziez1voyje7rb/GNSVMConf.png?dl=0&raw=1)
        3. En el menu izquierdo, seleccionar *VMware VMs* y elegir nuestra maquina virtual.
        ![GNSVM.png](https://www.dropbox.com/s/rlsjnysw95wsf4o/GNSVM.png?dl=0&raw=1)
        4. Una vez finalizado, seleccionamos el icono llamado *Reload all nodes*, para aplicar las nuevas configuraciones.
        ![GNSReload.png](https://www.dropbox.com/s/2ms7m3frpqxzdvl/GNSReload.png?dl=0&raw=1)
Una vez hecho esto, procedemos a asignar la IP.
1. Iniciar el dispositivo.
Al igual que con los otros dispositivos, se presiona click derecho y se elige la opción *Start*.
![VMStart.png](https://www.dropbox.com/s/3ddyzuhuo0bs0ko/VMStart.png?dl=0&raw=1)
Una vez iniciado, la conexión debera mostrarse verde.
2. Configurar la IP.
A diferencia de los otros dispositivos, esto lo haremos desde la maquina virtual en si.
    *   Estando en Tiny Linux, se abre el panel de control desde el dock de aplicaciones.
    ![VMPanel.png](https://www.dropbox.com/s/zqrfpfzpp5ip8hz/VMPanel.png?dl=0&raw=1)
    * Se elige la opción *Network* y colocamos la IP que se requiere en esta topología.
    ![ipvirttlp2.png](https://www.dropbox.com/s/ohlkqxeinc87c7q/ipvirttlp2.png?dl=0&raw=1)
    Se aplican los cambios y se sale.
   
## Pruebas
El siguiente comando se utiliza para comunicarse con otra maquina dentro de la red.
```sh
$ ping <IP>
```
![pingvp1vpc5.png](https://www.dropbox.com/s/iekrjowh4x37krn/pingvp1vpc5.png?dl=0&raw=1)
****
# GLOSARIO

* **ADDRESS**
Es la dirección IP que se le asigna a un dispositivo dentro de una red.
* **DHCP**
*Dynamic Host Configuration Protocol* es un protocolo usado por el protoco IP en redes, donde un servidor DHCP asigna una IP dinamicamente a otros en la red.
* **INTERFACE**
Componente que conecta un dispositivo a la red.
* **IP**
*Internet Protocol* es el protocolo principal en que se basa la internet, su funcion permite la comunicación en red.
* **MASK**
Combinación de bits que sirve para delimitar el ambito de una red-
* **PING**
Comando que permite hacer una verificación del estado de una determinada conexi´n de un host local con un equipo remoto en una red TCP/IP.
* **PUERTO**
Es un punto de comunicacion.
* **ROUTER**
Dispositivo de red que envia paquetes de datos entre redes de computadoras.
* **SWITCH**
Conmutador, dispositivo de conexión usado para conectar equipos en red, formando lo que se conoce como red de area loca *LAN* siguiendo el estandar Ethernet.
* **VPC**
*Virtual PC Simulator*, permite simular una PC ligera, con soporte para DHCP que apenas consume 2MB de RAM.