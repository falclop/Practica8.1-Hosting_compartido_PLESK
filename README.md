# Practica8.1-Hosting_compartido_PLESK
Creación de un servidor Plesk para Hosting Compartido
## Explicación de la práctica
Para esta práctica vamos a implementar en una instancia de Ubuntu 24.04 Server un servidor Plesk. 

[Plesk](https://es.wikipedia.org/wiki/Plesk) es una plataforma software de hosting que permite alojar y administrar sus aplicaciones web en un [servidor virtual privado (VPS)](https://es.wikipedia.org/wiki/Servidor_virtual_privado), en un [servidor dedicado](https://es.wikipedia.org/wiki/Servicio_de_alojamiento_dedicado) o en un servidor de un proveedor de servicios cloud.  

![](/images/dedicado.png)  

Estos servidores permiten una gran versatilidad a la hora de ofrecer hosting compartido o servicios multimedia para los usuarios, por lo que se colocan como una solución muy buena tanto a nivel profesional como usuario.  

## Creación del entorno
Lo primero de todo será crear una instancia en AWS con Ubuntu 24.04 Server con las siguientes características:  
- Nombre de la instancia: plesk.
- Imagen (AMI): Última versión disponible de Ubuntu Server.
- Arquitectura: x86.
- Tipo de instancia: t2.medium (2 vCPUs, 4 GB de RAM).
- Par de claves: vockey.
- Grupo de seguridad: Crear un grupo de seguridad para plesk.
- Almacenamiento: 30 GB de disco EBS.  
- Ip elástica.  

![](/images/1.png)

Después debemos crear un **grupo de seguridad** que llamaremos **sg_plesk** con las siguientes reglas de seguridad:  
- 22: SSH (TCP)
- 80: HTTP (TCP)
- 443: HTTPS (TCP)
- 21: FTP (TCP) - Puerto de control en los modos activo y pasivo
- 20: FTP (TCP) - Puerto de datos en el modo activo
- 49152 - 65535: Rango de puertos dinámicos para el modo pasivo (TCP)
- 25: SMTP (TCP)
- 465: SMTPS (TCP)
- 143: IMAP (TCP)
- 993: IMAPS (TCP)
- 110: POP3 (TCP)
- 995: POP3S (TCP)

![](/images/2.png)  

## Despliegue del servidor 