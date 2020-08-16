### TALLER LINUX 2020
##
El siguiente proyecto corresponde al trabajo obligatorio correspondiente al Taller Linux 2020 ORT.

### Presentación del Proyecto
##
El proyecto consta de dos partes:
 - Instalación de dos Servidores Linux.
 - Implementación de Playbook de Ansible para realizar diferentes tareas.

### Instalación servidores Lunux
##
Se crean dos servidores Linux, unos con distribución Centos8 y otro con distribución Ubuntu20.04.
Ambos incluyen los siguientes requerimientos:
  - Disco de 12 GB.
  - Partición física de 1G para /boot.
  - Volumen lógico de 5GB para /.
  - /var 3 GB para.
  - 2 GB para swap.
  - El resto de espacio libre para /home. 
  - Debe tener 2 interfaces de red definidas, una de ellas conectada a NAT y la otra a una red Interna que le permita conectarse al equipo bastión con Ansible. 
  - Debe existir un usuario ansible, con permisos de SUDO sin contraseña. 
  - Desde el equipo bastión, se debe copiar la clave pública hacia el servidor Linux implementado, para poder conectarse a él sin contraseña. 

### Implementación Playbook Ansible
## 
 Para la implementación de Playbook de Ansible, se cuenta con un equipo bastión con la herramienta Ansible instalada. Dicho equipo es un servidor Ubuntu20.04.
 Se implementan las siguientes configuraciones:
   1.	Instalar los paquetes correspondientes a un servidor web.
   2.	Generar un virtualhost a partir de un template que contenga la configuración para actuar como proxy reverso con balanceo de carga. 
   3.	Los valores para definir el clúster y los nodos que se van a balancear deben tomarse desde un archivo de variables. 
   4.	El servidor web debe reiniciarse si hay un cambio en la configuración del virtual host. 
   5.	El firewall debe estar activo y con los puertos correspondientes a los servicios http y https permitidos.
   6.	El estado de los servicios necesarios debe ser iniciados y habilitados. 
   7.	El playbook debe ser válido tanto para distribuciones CentOS como para distribuciones Ubuntu. 

### Repositorio GIT
El Playbook de Ansible y y todos los archivos necesarios se encuentran alojados en un repositorio de GitHub llamado “talleragosto2020”. 

### Link a repositorio GitHub

[talleragosto2020](https://github.com/nmigueza/talleragosto2020)

### Guía de instalación de Centos8

![Inicio de instalación](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\es1.jpg)
![Selección del Idioma](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\2.png)
![Destino de la instalación](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\3.png)
![Seleccionar disco físico](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\4.png)
![Configuración de particiones](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\5.png)
![usuarios](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\6.png)
![Establecer contraseña de root](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\7.png)
![Creación de usuario ansible](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\8.png)
![fin de instalación](C:\Users\nmigu\Desktop\ORT\Obligatorio\imagenes\9.png)


### Referencias

[Documentación de Ansible](https://docs.ansible.com/)
##
[Ansible Essentials](https://www.ansible.com/resources/webinars-training/introduction-to-ansible)
##
[GitHub](https://github.com/)



### Code

`code`

### Horizontal Rule

---



### Image



## Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

### Table

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

### Fenced Code Block

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

### Footnote

Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.

### Heading ID

### My Great Heading {#custom-id}

### Definition List

term
: definition

### Strikethrough

~~The world is flat.~~

### Task List

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

Agrega un link a un demo con el proyecto desplegado.
Si es requerido, agrega una lista con los pasos mínimos que se necesitan para clonar exitosamente el proyecto y echarlo a andar en local.
Explica qué debe ejecutarse para que sea posible instalarlo o instalar dependencias necesarias.
Se amable y agrega una imagen que indique cómo debe verse el proyecto luego de instalarse o un una vista previa de lo que estás presentando en código. Esta imagen puede estar dentro del mismo proyecto y de preferencia debería estar allí.
Finaliza con notas o apuntes que quisieras agregar, citando fuentes o dando agradecimientos a las personas que aportaron al proyecto que muestras.
Por favor muéstrame tus grandes readme's! Dedícales tiempo y diviértete haciéndolos, es como el landing de tu proyecto. Dale amorcito desde el corazón.