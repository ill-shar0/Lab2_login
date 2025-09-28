```markdown
# Laboratorio #2 - Implementación del Login en Laravel

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Descripción
Implementación de un sistema completo de autenticación desarrollado con el framework Laravel, siguiendo el patrón de arquitectura MVC (Modelo-Vista-Controlador). Utiliza Bootstrap para la interfaz de usuario, proporcionando una base sólida y escalable para aplicaciones web que requieran funcionalidades de registro y acceso de usuarios.

## Características Principales
- Sistema de autenticación tradicional con registro, inicio de sesión y recuperación de contraseña
- Interfaz responsive construida con Bootstrap para una experiencia de usuario adaptable
- Arquitectura MVC que garantiza una organización clara del código y separación de responsabilidades
- Middleware de seguridad para protección de rutas privadas
- Almacenamiento seguro de credenciales mediante base de datos MySQL

## Tecnologías Implementadas
- **Laravel 11** como framework PHP backend
- **Bootstrap 5** para el diseño frontend
- **Vite** para la compilación y gestión de assets
- **Eloquent ORM** para la gestión de base de datos
- **Sistema de migraciones** para control de versiones de base de datos

## Requisitos Previos

### Software Necesario
- PHP versión 8.0 o superior
- Composer última versión estable
- Laravel Installer
- Servidor web local (XAMPP, WampServer o Laragon)
- Base de datos MySQL/MariaDB
- Editor de código (Visual Studio Code recomendado)
- Node.js y NPM para compilación de assets

### Sistema Operativo
- Windows, Linux o macOS

## Instalación y Configuración

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/lab2-login-laravel.git
cd lab2-login-laravel
```

### 2. Instalar dependencias de PHP
```bash
composer install
```

### 3. Configurar entorno
```bash
cp .env.example .env
php artisan key:generate
```

### 4. Configurar base de datos
Editar el archivo `.env` con las credenciales de tu base de datos:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_base_datos
DB_USERNAME=root
DB_PASSWORD=
```

### 5. Instalar autenticación con Laravel UI
```bash
composer require laravel/ui
php artisan ui bootstrap --auth
```

### 6. Instalar dependencias de frontend
```bash
npm install
npm run dev
```

### 7. Ejecutar migraciones
```bash
php artisan migrate
```

### 8. Ejecutar el servidor de desarrollo
```bash
php artisan serve
```

La aplicación estará disponible en `http://localhost:8000`

## Arquitectura MVC en Laravel

### Modelos (Models)
- **Ubicación:** `app/Models/`
- **Función:** Gestionan los datos y la lógica de negocio
- **Ejemplo:** `User.php` - Maneja la información de usuarios y autenticación

### Vistas (Views)
- **Ubicación:** `resources/views/`
- **Función:** Interfaz de usuario (archivos .blade.php)
- **Ejemplos:** 
  - `auth/login.blade.php` - Vista del formulario de login
  - `auth/register.blade.php` - Vista del formulario de registro
  - `layouts/app.blade.php` - Layout principal de la aplicación

### Controladores (Controllers)
- **Ubicación:** `app/Http/Controllers/`
- **Función:** Gestionan las peticiones HTTP y la lógica de aplicación
- **Ejemplos:**
  - `LoginController.php` - Controla el proceso de autenticación
  - `RegisterController.php` - Controla el proceso de registro
  - `HomeController.php` - Controla el dashboard después del login

### Rutas (Routes)
- **Ubicación:** `routes/web.php`
- **Función:** Definen las URLs y endpoints de la aplicación
- **Ejemplo:** 
```php
Route::get('/login', [LoginController::class, 'showLoginForm']);
Route::post('/login', [LoginController::class, 'login']);
Route::post('/logout', [LoginController::class, 'logout']);
```

## Base de Datos

### Migraciones
Comandos utilizados para la gestión de la base de datos:
```bash
# Ver estado de migraciones
php artisan migrate:status

# Ejecutar migraciones pendientes
php artisan migrate

# Revertir la última migración
php artisan migrate:rollback

# Reiniciar completamente la base de datos
php artisan migrate:fresh
```

### Estructura de Tablas Principales
- **users:** Almacena información de usuarios (nombre, email, contraseña hash, timestamps)
- **password_reset_tokens:** Maneja tokens para recuperación de contraseñas
- **failed_jobs:** Registra jobs en cola que han fallado
- **personal_access_tokens:** Gestiona tokens para API authentication

### Backup de Base de Datos
- El archivo de backup se encuentra en: `database/backup/lab2_backup.sql`

## Dificultades y Soluciones Encontradas

### Problema 1: Error de conexión con MySQL en XAMPP
**Descripción:** Se presentaron inconvenientes al inicializar MySQL desde el servidor XAMPP debido a conflictos con los puertos.

**Solución:**
- Primero se intentó cambiar el puerto y actualizar Laravel, pero esta solución no funcionó
- Posteriormente se desinstaló el paquete completo y se volvió a instalar
- La configuración inicial no funcionaba correctamente, pero después de ajustar la configuración específica, el servicio se estableció correctamente

### Problema 2: Error "Internal Server Error 500" al registrar usuarios
**Descripción:** Al intentar registrar nuevos usuarios en Laravel, se presentaba un error interno del servidor.

**Solución:**
- Investigación reveló que la causa era el uso de palabras clave obsoletas en el código
- Se modificaron todos los archivos de código que incluían la función `middleware()`
- Se cambió de `App\Http\Controllers\Controller` a `use Illuminate\Routing\Controller;`

### Problema 3: Conflictos con controladores después del cambio de namespace
**Descripción:** Después de realizar el cambio a `Illuminate\Routing\Controller`, surgieron múltiples conflictos con otros controladores del sistema.

**Solución:**
- Se tomó la decisión de eliminar completamente el proyecto
- Se volvió a levantar el proyecto desde cero
- Se aplicaron las correcciones necesarias desde el inicio del desarrollo

### Problema 4: Assets de frontend no cargan correctamente
**Descripción:** Los archivos CSS y JavaScript no se visualizaban correctamente en las vistas.

**Solución:**
- Ejecutar `npm run dev` para compilar los assets
- Verificar las rutas correctas en las vistas Blade usando `{{ asset() }}`
- Limpiar la caché de configuración con `php artisan config:clear`

### Problema 5: Error en migraciones por longitud de cadena
**Descripción:** Error al ejecutar migraciones relacionado con la longitud máxima de cadenas.

**Solución:**
- Agregar en `AppServiceProvider.php` en el método `boot()`:
```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

## Comandos Importantes Utilizados

### Configuración del entorno
```bash
# Generar clave de aplicación
php artisan key:generate

# Limpiar caché de configuración
php artisan config:clear

# Cachear configuración para producción
php artisan config:cache
```

### Desarrollo frontend
```bash
# Compilar assets en modo desarrollo
npm run dev

# Compilar assets en modo producción
npm run build

# Compilar y observar cambios en tiempo real
npm run watch
```

### Gestión de la aplicación
```bash
# Limpiar caché de rutas
php artisan route:clear

# Limpiar caché de vistas
php artisan view:clear

# Limpiar toda la caché
php artisan cache:clear
```

## Estructura del Proyecto

```
lab2-login-laravel/
├── app/
│   ├── Http/
│   │   └── Controllers/
│   │       ├── Auth/
│   │       │   ├── LoginController.php
│   │       │   ├── RegisterController.php
│   │       │   └── ...
│   │       └── Controller.php
│   └── Models/
│       └── User.php
├── config/
│   └── auth.php
├── database/
│   ├── migrations/
│   │   ├── 2014_10_12_000000_create_users_table.php
│   │   ├── 2014_10_12_100000_create_password_reset_tokens_table.php
│   │   └── ...
│   └── backup/
│       └── lab2_backup.sql
├── resources/
│   └── views/
│       ├── auth/
│       │   ├── login.blade.php
│       │   ├── register.blade.php
│       │   └── ...
│       └── layouts/
│           └── app.blade.php
├── routes/
│   └── web.php
├── .env.example
├── composer.json
└── README.md
```

## Referencias Utilizadas

1. **Documentación Oficial de Laravel** - https://laravel.com/docs
2. **Laravel Authentication** - https://laravel.com/docs/authentication
3. **Stack Overflow** - Soluciones a problemas comunes de Laravel
4. **Laravel News** - Tutoriales y mejores prácticas
5. **Laracasts** - Video tutorials sobre Laravel y PHP

## Información Académica

### Universidad Tecnológica de Panamá
**Facultad de Ingeniería de Sistemas Computacionales**  
**Departamento de Ingeniería de Software**  
**Campus Victor Levi Sasso**

### Datos del Estudiante
- **Nombre:** Gabriela Takata
- **Cédula:** 8-991-822
- **Correo Institucional:** [correo@utp.ac.pa]
- **Formación Universitaria:** Licenciatura de Ingeniería de Software
- **Asignatura:** Ingeniería Web
- **Grupo/Salón:** 15F131
- **Semestre:** II Semestre 2025

### Información del Laboratorio
- **Instructor:** Ing. Irina Fong
- **Título de la experiencia:** Primer acercamiento al framework Laravel y exploración de su estructura de trabajo
- **Tema:** Introducción al framework Laravel: estructura de carpetas y patrón Modelo-Vista-Controlador (MVC)
- **Fecha de inicio:** 01 de septiembre de 2025
- **Fecha límite de entrega:** 15 de septiembre de 2025
- **Fecha de ejecución:** Septiembre 2025

### Objetivos Cumplidos
- [x] Identificar la estructura básica de un proyecto en Laravel
- [x] Comprender la organización del framework bajo el patrón MVC
- [x] Reconocer la importancia de la arquitectura MVC en desarrollo web moderno
- [x] Implementar sistema completo de autenticación
- [x] Gestionar base de datos con migraciones
- [x] Resolver problemas comunes de configuración y desarrollo

## Conclusión

El laboratorio fue fundamental para comprender el ecosistema de Laravel y su arquitectura MVC. Se aprendió la criticalidad de una configuración precisa del entorno, el ciclo de vida de una petición HTTP (rutas, controladores, middleware) y la gestión de namespaces en PHP. La resolución de errores, como la importación de clases, reforzó la importancia del pensamiento crítico y la perseverancia, consolidando así los fundamentos del desarrollo web moderno y las competencias esenciales de un ingeniero de software.

El proyecto sirve como punto de partida para aplicaciones web que requieran autenticación de usuarios, demostrando las mejores prácticas de desarrollo con Laravel y la integración efectiva de herramientas modernas de frontend y backend.

---

**Este laboratorio ha sido desarrollado como parte del curso de Ingeniería Web en la Universidad Tecnológica de Panamá, cumpliendo con todos los requisitos establecidos en la guía de laboratorio.**

**© 2025 - Universidad Tecnológica de Panamá - Todos los derechos reservados.**
```
