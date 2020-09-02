# REPORTES
## Calculo de colisiones

* **HUB:**
1 Dominio de colision
1 Dominio de broadcast
* **SWITCH:**
n Dominios de colisión (n = # puertos conectados)
1 Dominio de broadcast
* **ROUTER:**
1 Dominio de colision
1 Dominio de broadcast
* Por cada interface conectada

![dominioscolisiones.png](https://www.dropbox.com/s/asdv6c59eqvfzys/dominioscolisiones.png?dl=0&raw=1)

Tenemos:
9 dominios de colisión
3 dominios de broadcast

### Creación del proyecto

Creamos el proyecto en GNS3, nuestro proyecto se llamara Redes1-Practica2_201318652.

![creando_proyecto.png](https://www.dropbox.com/s/ne5vb82p9k18hvq/creando_proyecto.png?dl=0&raw=1)

## Captura de paquetes

### VPC1
Para comprobar que si hay comunicación con los equipos en la red, se utiliza el software WireShark, el cual muestra el transito en la red.

Para este proposito, se esta analizando el transito en la conexión de la VPC1 a su SW1.

* **Ping VPC1 - VPC5**
![vpc1vpc5.png](https://www.dropbox.com/s/med1w7c9qq5kyso/vpc1vpc5.png?dl=0&raw=1)
* **Ping VPC4 - VPC1**
![vpc4vpc1.png](https://www.dropbox.com/s/xrn72473c53jw1p/vpc4vpc1.png?dl=0&raw=1)
