# Avatar Manager

Sistema de gestión de avatares desarrollado en PHP puro, que permite a los usuarios iniciar sesión, visualizar, cargar y descargar imágenes de avatar según su rol asignado.

## 📋 Descripción del Proyecto

**Avatar Manager** es una aplicación web que implementa un sistema de autenticación basado en roles con las siguientes funcionalidades principales:

- **Sistema de login/logout** con sesiones y cookies
- **Gestión de usuarios** con persistencia en archivos de texto
- **Control de acceso basado en roles** (básico y avanzado)
- **Galería de avatares** con visualización y descarga
- **Carga de nuevos avatares** (solo usuarios avanzados)
- **Perfil de usuario** con actualización de contraseña
- **Contador de visitas** por usuario

## 🗂️ Estructura de Directorios

```
Avatar-Manager/
│
├── avatars/                    # Directorio donde se almacenan las imágenes de avatar
│
├── files/                      # Archivos de persistencia de datos
│   └── users.txt              # Base de datos de usuarios (formato: username;password;role;visits)
│
├── fn-php/                     # Funciones y lógica de negocio
│   ├── fn-avatars.php         # Funciones para listar avatares disponibles
│   ├── fn-roles.php           # Control de permisos y acceso por roles
│   ├── fn-users.php           # Funciones CRUD para gestión de usuarios
│   ├── upload.php             # Script de procesamiento de carga de archivos
│   └── download.php           # Script de descarga segura de avatares
│
├── includes/                   # Componentes compartidos de la interfaz
│   ├── topmenu.php            # Barra de navegación con menú dinámico según rol
│   └── footer.php             # Pie de página de la aplicación
│
├── index.php                   # Página principal: login y galería de avatares
├── profile.php                 # Página de perfil de usuario
├── avatarManagement.php        # Página de gestión (carga) de avatares
└── logout.php                  # Script de cierre de sesión
```

## 🚀 Cómo Arrancar el Proyecto

### Requisitos Previos

- **PHP 7.4+** instalado
- Servidor web (Apache, Nginx, o el servidor integrado de PHP)
- Permisos de escritura en los directorios `avatars/` y `files/`

### Instalación y Configuración

1. **Clona el repositorio:**
   ```bash
   git clone https://github.com/alba-mu/Avatar-Manager.git
   cd Avatar-Manager
   ```

2. **Asegúrate de que los directorios tienen permisos de escritura:**
   ```bash
   chmod 755 avatars/
   chmod 755 files/
   chmod 666 files/users.txt
   ```

3. **Verifica el archivo de usuarios**  
   El archivo `files/users.txt` debe existir con el formato:
   ```
   username;password;role;visits
   user1;password1;advanced;0
   user2;pass2;basic;0
   ```

4. **Arranca el servidor local:**

   **Opción 1: Servidor integrado de PHP**
   ```bash
   php -S localhost:8000
   ```

   **Opción 2: XAMPP/WAMP/MAMP**
   - Coloca el proyecto en la carpeta `htdocs/` o `www/`
   - Accede desde `http://localhost/Avatar-Manager/`

5. **Abre tu navegador y accede a:**
   ```
   http://localhost:8000/index.php
   ```

## 👥 Sistema de Roles y Permisos

El proyecto implementa un sistema de control de acceso con dos roles:

| Rol       | Permisos                                                    |
|-----------|-------------------------------------------------------------|
| **basic** | Ver galería de avatares, descargar, acceder a su perfil    |
| **advanced** | Todos los permisos de basic + cargar nuevos avatares     |
| **guest** | Solo ver página de login                                    |

El control de permisos se gestiona mediante la función `isGranted()` en `fn-php/fn-roles.php`.

## 📄 Archivos Principales

### **index.php**
- Punto de entrada de la aplicación
- Muestra formulario de login si el usuario no está autenticado
- Muestra galería de avatares si el usuario está autenticado
- Valida credenciales y gestiona sesiones

### **profile.php**
- Permite al usuario ver su información
- Actualización de contraseña
- Muestra contador de visitas
- Requiere autenticación

### **avatarManagement.php**
- Formulario de carga de nuevos avatares (solo usuarios avanzados)
- Valida tipo de archivo (solo PNG y JPEG)
- Muestra galería completa de avatares disponibles

### **logout.php**
- Cierra la sesión del usuario
- Elimina cookies de sesión
- Redirige a página de confirmación

## 🔧 Funciones Principales

### Gestión de Usuarios (`fn-php/fn-users.php`)
- `searchUser($username)`: Busca un usuario en la base de datos
- `insertUser($username, $password, $role, $visits)`: Inserta nuevo usuario
- `updateUser($username, $password, $role, $visits)`: Actualiza información del usuario

### Gestión de Avatares (`fn-php/fn-avatars.php`)
- `listAvatars()`: Lista todos los avatares disponibles (PNG/JPEG)

### Control de Roles (`fn-php/fn-roles.php`)
- `isGranted($role, $page)`: Verifica si un rol tiene acceso a una página

## 🎨 Tecnologías Utilizadas

- **Backend:** PHP (sin frameworks)
- **Frontend:** HTML5, Bootstrap 5.3.3
- **Persistencia:** Archivos de texto plano
- **Autenticación:** Sesiones PHP + Cookies
- **Seguridad:** Sanitización de inputs, validación de tipos de archivo

## 🔐 Seguridad

- Sanitización de entradas con `filter_input()`
- Validación de tipos MIME para cargas de archivos
- Uso de `basename()` para prevenir path traversal
- Control de acceso basado en roles
- Gestión segura de sesiones

## 📝 Formato del Archivo de Usuarios

El archivo `files/users.txt` utiliza punto y coma (`;`) como delimitador:

```
username;password;role;visits
admin;admin123;advanced;5
user;pass;basic;2
```

⚠️ **Nota:** En producción, las contraseñas deberían estar hasheadas (ej. con `password_hash()`).

## 🖼️ Formatos de Avatar Soportados

- **JPEG** (image/jpeg)
- **PNG** (image/png)

Los archivos se validan tanto en carga como en descarga para asegurar que sean imágenes válidas.


## 📜 Licencia

Este proyecto fue desarrollado con fines educativos por **Alba Muñoz**.

## 📧 Contacto

Para preguntas o sugerencias, puedes contactar al autor a través de GitHub.
