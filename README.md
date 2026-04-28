# Laboratorio 2: Sistema de Autenticación con Laravel 11

Este proyecto es una aplicación web desarrollada con **Laravel 11**, configurada para funcionar en un entorno local utilizando **WampServer**. Incluye un sistema completo de inicio de sesión (Login) y registro de usuarios utilizando **Bootstrap**.

## 1. Requisitos del Sistema
* **Servidor:** WampServer 3.3.5+.
* **PHP:** 8.3.28 (Versión actualizada para compatibilidad con Laravel 11).
* **Base de Datos:** MySQL 8.4.7 (Puerto 3308).
* **Gestor de paquetes:** Composer y Node.js (NPM).

## 2. Proceso de Instalación 
## 2.1 Instalación de composer y laravel installer
  * **1.** Se abrió el CMD de Windows en modo administrador.
  * **2.** Se navegó hasta la carpeta donde WampServer guarda los proyectos web:
      ```
      C:\Windows\System32>cd..
      C: \Windows>cd..
      C:\>cd wamp64
      C:\wamp64>cd www
      ```
* **3. Creación del proyecto:** Se ejecutó el comando para iniciar un nuevo proyecto de Laravel llamado "Lab3":
      ```
      laravel new Lab3
      ```
      *(Durante la instalación se seleccionó el starter kit de Laravel UI con Bootstrap).*

## 3. Configuración de Base de Datos
Debido a la actualización de MySQL en WampServer, se realizaron ajustes críticos para permitir la comunicación entre el framework y el servidor:

* **Puerto:** Se cambió el puerto por defecto (3306) al **3308**, ya que es el que utiliza MySQL 8.4 en las versiones nuevas de Wamp.
* **Usuario y Permisos:** Se verificó el acceso del usuario `root` sin contraseña.
* **Archivo .env:**
  ```env
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3308
  DB_DATABASE=lab3
  DB_USERNAME=root
  DB_PASSWORD=

## 4. Solución de Errores Técnicos (Troubleshooting)
Durante el desarrollo se presentaron y resolvieron los siguientes inconvenientes:

* **4.1: Error de Conexión (Access Denied)**
El sistema denegaba el acceso por el uso del plugin de autenticación moderno de MySQL 8. Se solucionó limpiando el caché de configuración:
```
php artisan config:clear
```

* **4.2 Error: "Specified key was too long" (1071)**
Este error ocurre por la longitud de los índices en MySQL al usar el juego de caracteres utf8mb4. Se corrigió modificando el archivo ```app/Providers/AppServiceProvider.php:```
```
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```
* **4.3 Compilación de Bootstrap**
Para activar los estilos visuales del sistema de Login y Register, se ejecutó el compilador de activos (Vite):
```
npm install
npm run build
```

## 5. Ejecución del Proyecto
Para visualizar la aplicación, se debe iniciar el servidor de desarrollo de Laravel:
```
php artisan serve
```
Luego, acceder  a: ```http://127.0.0.1:8000```

Nota: El acceso a la base de datos vía web se realiza a través de ```http://localhost/phpmyadmin5.2.3/``` según el alias configurado en el servidor Apache.
