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
##
El Playbook de Ansible y y todos los archivos necesarios se encuentran alojados en un repositorio de GitHub llamado “talleragosto2020”. 

### Link a repositorio GitHub

[talleragosto2020](https://github.com/nmigueza/talleragosto2020)

### Guía de instalación de Centos8
##
   - Iniciar la instalación.
   - Seleccionar el idioma.
   - Configurar destino de la instalación.
   - Seleccionar disco físico y modo de configuración.
   - Configurar particiones.
   - Establecer contraseña de root.
   - Crear usuario ansible.
   - Reiniciar para finalizar la instalación.

### Guía de instalación de Ubuntu20.04
##
   - Iniciar la instalación.
   - Seleccionar el idioma.
   - Seleccionar idioma del teclado.
   - Seleccionar disco físico y la opción de configurarlo como un grupo LVM.
   - Configurar particiones.
   - Establecer nombre de equipo y crear usuario ansible.
   - Reiniciar para finalizar la instalación.

[^1] Las guías de instalación descriptas anteriormente corresponden a los pasos principales en la instalación de los sistemas operativos. Existen también otros pasos intermedios que deben dejarse con las configuraciones por defecto.

### Creación de Playbook Ansible
##
Todas las configuraciones descriptas anteriormente aplican para familias de servidores RedHat y Debian. RedHat incluye la distribución Centos y Debian incluye la distribución Ubuntu utilizadas en este proyecto.

De esta forma, esta implementación es más genérica y aplica también a otras distribuciones diferentes de Centos y Ubuntu, siempre que sean de las familias definidas.

### Estructura del playbook
##
El playbook de Ansible creado cuenta con los siguientes componentes:
   - Archivo de configuración local ansible.cfg.
   - Archivo inventario, que contiene la lista de equipos a los que se le aplica el playbook.
   - Archivo playbook.yml con las configuraciones correspondientes para la ejecución. Contiene la llamada a los diferentes roles creados y también la configuración para la implementación de Virtual Host con proxy Reverso y Balanceo de Carga.
   - Directorio roles que contiene las configuraciones de los diferentes roles definidos.
   - Directorios vars donde se aloja el archivo de variables, loadbalancer_vars.yml, para configuración de Virtual Host para Proxy Reverso y Balanceo de Carga.
   - Directorio templates que contiene el archivo loadbalancer.j2 que contiene la estructura del archivo de Virtual Host generado a partir del playbook.yml.
   - Archivo README.md.

### Archivo ./taller_2020/ansible.cfg
##
Se configuran los siguientes parámetros:
`inventory       = ./inventario`
`sudo_user      = ansible`
`roles_path    = ./roles:/etc/ansible/roles`

### Archivo ./taller_2020/inventario
##
`[webserver]`
`centos1 ansible_host=192.168.227.7`
`ubuntu1 ansible_host=192.168.227.9`

### Archivo ./taller_2020/playbook.yml
Contiene las llamadas a los roles:
    `- role: apache-redhat`
     ` when: ansible_facts['os_family'] == "RedHat"`
    `- role: apache-debian`
     ` when: ansible_facts['os_family'] == "Debian"`
    `- role: modulos-apache`

Y también contiene las tareas de loadbalancer:

Para familia RedHat:
  `- name: Create loadbalancer configuration for RedHat`
   ` template:`
`      src: templates/loadbalancer.j2`
 `     dest: /etc/httpd/vhost.d/loadbalancer.conf`
  `    owner: root`
   `   mode: '0644'`
    `when: ansible_facts['os_family'] == "RedHat"`
    `notify: Restart httpd`

Para familia Debian:
 ` - name: Create loadbalancer configuration for Debian`
  `  template:`
   `   src: templates/loadbalancer.j2`
    `  dest: /etc/apache2/sites-enabled/000-default.conf`
     ` owner: root`
      `mode: '0644'`
    `when: ansible_facts['os_family'] == "Debian"`
    `notify: Restart apache`

### Roles definidos
##
Se definen los siguientes roles:

### apache-redhat
##
Aplica a servidores de la familia Redhat y contiene las tareas correspondientes a:
   - Instalación de Apache Server.
   - Creación del directorio para virtual Host.
   - Se agrega dicho directorio a la configuración de Apache, archivo /etc/httpd/conf/httpd.conf.
   - Se inicia y habilita el servicio hhtpd.
   - Se configura el firewall para que acepte conexxiones http y https.

### apache-debian
##
Aplica a servidores de la familia Debian y contiene las tareas correspondientes a:
   - Instalación de Apache Server.
   - Se inicia y habilita el servicio hhtpd.
   - Se configura el firewall para que acepte conexxiones http y https.

### modulos-apache
Aplica a servidores de ambas familias y contiene la habilitación de los módulos de Apache que son necesarios para configurar Proxy Reverso y Balanceo de Carga.
Estos módulos son:
    - proxy
    - proxy_http
    - proxy_balancer
    - lbmethod_byrequests

### Archivo de Variables
##
Archivo ./taller_2020/loadbalancer_vars.yml
`nombre_cluster: balanceador`
`nodo1: nodo1.lab.ort`
`nodo2: nodo2.lab.ort`
`puerto1: 8080`
`puerto2: 8080`
`red_autorizada: 192.168.227.0/24`

### Archivo ./taller_2020/loadbalancer.j2
Contiene la configuración de virtual Host para Proxy Reverso y Balanceador
`<VirtualHost *:80>`
 ` <Proxy balancer://{{ nombre_cluster }}>`
     ` BalancerMember http://{{ nodo1 }}:{{ puerto1 }}`
    `  BalancerMember http://{{ nodo2 }}:{{ puerto2 }}`
  `    Require all granted`
 ` </Proxy>`
 `ProxyPreserveHost On`
 `ProxyPass /balancer-manager !`
 `ProxyPass / balancer://{{ nombre_cluster }}/`
 `ProxyPassReverse / balancer://{{ nombre_cluster }}/`
  `<Location "/balancer-manager">`
   `  SetHandler balancer-manager`
     `Require ip {{ red_autorizada }}`
  `</Location>`
`</VirtualHost>`

### Ejecución de Playbook
Para la ejecución del Playbook es necesario correr el sifguiente comando en el servidos bastión de Ansible:
Directorio: ./taller_2020
Comando: `ansible-playbook playbook.yml --ask-become-pass`

### Otros comandos útiles:
##
Para chequear sintaxis de Playbook: `ansible-playbook playbook.yml --syntax.check --ask-become-pass`

Para realiizar un drive run: `ansible-playbook playbook.yml --check --ask-become-pass`

### Referencias

[Documentación de Ansible](https://docs.ansible.com/)
##
[Ansible Essentials](https://www.ansible.com/resources/webinars-training/introduction-to-ansible)
##
[GitHub](https://github.com/)

### Autor
##
Lic. Nancy Miguez








