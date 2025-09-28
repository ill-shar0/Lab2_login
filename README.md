# Laboratorio #2 - Implementación del Login en Laravel

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Descripción
Implementación de un sistema de autenticación en Laravel utilizando la arquitectura MVC como parte del Laboratorio #2 de Ingeniería Web.

## Requisitos Previos

### Software Necesario
- PHP versión 8.0 o superior
- Composer última versión estable
- Laravel Installer
- Servidor web local (XAMPP utilizado en este proyecto)
- Base de datos MySQL/MariaDB
- Editor de código (Visual Studio Code recomendado)

### Sistema Operativo
- Windows, Linux o macOS

## Instalación y Configuración

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/lab2-login-laravel.git
cd lab2-login-laravel

 Instalar dependencias
bash
composer install
3. Configurar entorno
bash
cp .env.example .env
php artisan key:generate
4. Configurar base de datos
Editar el archivo .env:

env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_base_datos
DB_USERNAME=root
DB_PASSWORD=
5. Instalar autenticación (con Laravel UI)
bash
composer require laravel/ui
php artisan ui bootstrap --auth
npm install
npm run dev
6. Ejecutar migraciones
bash
php artisan migrate
7. Ejecutar el servidor
bash
php artisan serve
Arquitectura MVC en Laravel
Modelos (Models)
Ubicación: app/Models/

Función: Gestionan los datos y la lógica de negocio

Ejemplo: User.php - Maneja la información de usuarios

Vistas (Views)
Ubicación: resources/views/

Función: Interfaz de usuario (archivos .blade.php)

Ejemplo: auth/login.blade.php - Vista del formulario de login

Controladores (Controllers)
Ubicación: app/Http/Controllers/

Función: Gestionan las peticiones HTTP

Ejemplo: LoginController.php - Controla el proceso de autenticación

Rutas (Routes)
Ubicación: routes/web.php

Función: Definen las URLs de la aplicación

Ejemplo:

php
Route::get('/login', [LoginController::class, 'showLoginForm']);
Base de Datos
Migraciones
Comandos utilizados para crear las tablas:

bash
php artisan migrate:status  # Ver estado de migraciones
php artisan migrate        # Ejecutar migraciones
Estructura de Tablas
users: Almacena información de usuarios

password_reset_tokens: Maneja recuperación de contraseñas

failed_jobs: Registra jobs fallidos

Dificultades y Soluciones
Problema 1: Error de conexión con MySQL
Descripción: Inconvenientes al inicializar MySQL desde XAMPP debido a conflictos con los puertos

Solución: Se intentó cambiar de puerto y actualizar Laravel sin éxito. Finalmente se desinstaló y reinstaló el paquete, configurándolo correctamente para que funcionara.

Problema 2: Error "Internal Server Error" al registrar
Descripción: Error interno del servidor al intentar registrar usuarios en Laravel

Solución: Investigación reveló que era por uso de palabras clave obsoletas. Se modificaron todos los archivos que incluían la función middleware(), cambiando App\Http\Controllers\Controller a use Illuminate\Routing\Controller;

Problema 3: Conflictos con controladores después del cambio
Descripción: Después de cambiar a Illuminate\Routing\Controller, surgieron conflictos con otros controladores

Solución: Se eliminó el proyecto y se volvió a levantar desde cero, aplicando las correcciones necesarias desde el inicio.

Referencias
Documentación Oficial de Laravel - https://laravel.com/docs

Laravel Authentication - https://laravel.com/docs/authentication

Stack Overflow - Soluciones a problemas comunes de Laravel

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
