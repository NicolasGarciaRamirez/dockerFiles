# dockerFiles
 
Cuando se clone un proyecto de GITHUB este no viene con los paquetes de laravel
instalados, para hacer esta instalacion del "vendor" se debe ejecutar el
siguiente comando:

```
docker run --rm -v "$(pwd):/var/www/html" -w /var/www/html laravelsail/php81-composer:latest composer install --ignore-platform-reqs
```

La seccion de `php81-composer:latest` se debe de acomodar con la version de php
**(74, 80, 81)**

**NOTA:** Se debe de estar ubicado dentro de la carpeta del proyecto en la
terminal.

- Si el proyecto es echo con laravel 6, se debe de copiar el contenido que está
  dentro de la carpeta de laravel_6 en la raiz del proyecto.

<h2>Permisos</h2>
Se debe de dar permisos a la carpeta del proyecto para que no haya problemas luego al crear un archivo o hacer un compose dump, se debe de estar dentro del proyecto y darle:

```
sudo chmod 775 -R .
```

<h2>Alias</h2>
Para crear los alias que se usaran para sail y exec se debe de abrir bin con el siguiente comando dentro del WSL

```
vim ~/.bashrc
```

- Para editar en vim se usa la tecla "i"
- Para salir de la edicion se usa la tecla "ESC"

En la ultima linea de vim bajando con la flecha se debe de pegar las 2 lineas:

```
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
alias exec='./exec'
```

- Para guardar en vim se usa el comando:

```
:wq
```

Se debe luego reiniciar la terminal.

<h2>.env</h2>
Se debe crear el .env con el .env que esta en la carpeta laravel_6
y los campos se deben editar tanto con el puerto de escucha de la aplicacion como con el nombre del contenedor respectivamente:

- APP_PORT
- APP_SERVICE

<hr>

- Para ejecutar el `docker-compose.yml` se debe usar el comando:

```
sail up -d --build
ó
exec up -d --build
```

La bandera `--build` se debe usar cuando en el archivo del `docker-compose.yml`
hay una seccion build que usa un `dokerfile` si no existe no se coloca en el
anterior comando.

- Para ejecutar los comandos (artisan, npm, composer etc..) se usa:

```
sail <comando>
```

ó

```
exec <comando>
```

<h2>EJ:</h2>

```
$ sail php artisan make:controller HomeController
```

ó

```
$ exec npm i
```

<hr>

- Si se necesita entrar al contenedor para ejecutar algo de php, npm o composer
  se debe usar el siguiente comando:

```
docker exec -it <nombre_contenedor> bash
```

- La ip de docker para comunicase entre contenedores es:

```
172.17.0.1:<puerto_contenedor>
```

**NOTA:** Para que los contenedores se comuniquen entre ellos se debe de usar la
misma red entre contenedores.
