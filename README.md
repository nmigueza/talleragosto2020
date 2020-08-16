### Bold
TALLER LINUX 2020
##
El siguiente proyecto corresponde al trabajo obligatorio correspondiente al Taller Linux 2020 ORT.
**bold text**
Proyecto

### Italic

*El proyecto consta de dos partes:
 - Instalación de Servidor Linux.
 - Implementación de Playbook de Ansible para realizar diferentes tareas.

Además, es necesario contar con por lo menos dos servidores:
 - El servidor Linux que se debe implementar.
 - 	Equipo bastión con la herramienta Ansible instalada.
*
**bold text**
Instalación servidor Lunux
### Italic
* - Disco de 12 GB.
  - Partición física de 1G para /boot.
  - Volumen lógico de 5GB para /.
  - 	/var 3 GB para.
  - 2 GB para swap.
  - El resto de espacio libre para /home. 
  - Debe tener 2 interfaces de red definidas, una de ellas conectada a NAT y la otra a una red Interna que le permita conectarse al equipo bastión con Ansible. 
  - Debe existir un usuario ansible, con permisos de SUDO sin contraseña. 
  - Desde el equipo bastión, se debe copiar la clave pública hacia el servidor Linux implementado, para poder conectarse a él sin contraseña. 

  **bold text**
  Implementación Playbook Ansible
  ## Italic
  *1.	Instalar los paquetes correspondientes a un servidor web.
   2.	Generar un virtualhost a partir de un template que contenga la configuración para actuar como proxy reverso con balanceo de carga. 
   3.	Los valores para definir el clúster y los nodos que se van a balancear deben tomarse desde un archivo de variables. 
   4.	El servidor web debe reiniciarse si hay un cambio en la configuración del virtual host. 
   5.	El firewall debe estar activo y con los puertos correspondientes a los servicios http y https permitidos.
   6.	El estado de los servicios necesarios debe ser iniciados y habilitados. 
   7.	El playbook debe ser válido tanto para distribuciones CentOS como para distribuciones Ubuntu. 
   8.	El playbook y todos los archivos necesarios deben ser subidos a un repositorio GIT llamado “talleragosto2020”. 
   9.	El repositorio, además de los archivos de Ansible solicitados, debe contar con un archivo README.md que describa el funcionamiento del Playbook y como debe ser utilizado.


### Blockquote

> blockquote

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- First item
- Second item
- Third item

### Code

`code`

### Horizontal Rule

---

### Link

[title](https://www.example.com)

### Image

![alt text](image.jpg)

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
El primer título es el nombre de tu proyecto.
El texto siguiente es una descripción simple y corta del contexto de tu proyecto.
Agrega un link a un demo con el proyecto desplegado.
Si es requerido, agrega una lista con los pasos mínimos que se necesitan para clonar exitosamente el proyecto y echarlo a andar en local.
Explica qué debe ejecutarse para que sea posible instalarlo o instalar dependencias necesarias.
Se amable y agrega una imagen que indique cómo debe verse el proyecto luego de instalarse o un una vista previa de lo que estás presentando en código. Esta imagen puede estar dentro del mismo proyecto y de preferencia debería estar allí.
Finaliza con notas o apuntes que quisieras agregar, citando fuentes o dando agradecimientos a las personas que aportaron al proyecto que muestras.
Por favor muéstrame tus grandes readme's! Dedícales tiempo y diviértete haciéndolos, es como el landing de tu proyecto. Dale amorcito desde el corazón.