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

### 2. Istalar dependencias de PHP
```bash
composer install

### 3. Configurar entorno: 
```bash
cp .env.example .env
php artisan key:generate

### 4. Configurar base de datos
```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_base_datos
DB_USERNAME=root
DB_PASSWORD=

### 5. Instalar autenticación con Laravel UI
```bash
composer require laravel/ui
php artisan ui bootstrap --auth
