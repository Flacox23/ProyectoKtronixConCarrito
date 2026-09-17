# Ktronix

Tienda en línea de electrodomésticos y tecnología (celulares, laptops, cámaras, neveras, lavadoras, etc.) hecha en PHP puro con MySQL. Tiene la parte del cliente (catálogo, carrito, wishlist, checkout, cuenta de usuario) y un panel de administración aparte para gestionar productos, pedidos, mensajes y cuentas.

## Tecnologías usadas

- **PHP** (sin framework, con PDO para la conexión a la base de datos)
- **MySQL / MariaDB**
- **HTML, CSS y JavaScript** propios (`css/style.css`, `js/script.js`, y sus equivalentes `admin_*` para el panel)
- **Font Awesome** y **Swiper.js** cargados por CDN (se usan para los íconos y los carruseles de imágenes)

## Estructura del proyecto

```
ktronix/
├── admin/                  # Panel de administración
│   ├── admin_login.php
│   ├── dashboard.php
│   ├── products.php
│   ├── update_product.php
│   ├── placed_orders.php
│   ├── users_accounts.php
│   ├── admin_accounts.php
│   ├── register_admin.php
│   ├── update_profile.php
│   └── messages.php
├── components/              # Partes reutilizables (header, footer, conexión, etc.)
│   ├── connect.php          # Conexión a la base de datos
│   ├── user_header.php
│   ├── admin_header.php
│   ├── footer.php
│   ├── user_logout.php
│   ├── admin_logout.php
│   └── wishlist_cart.php
├── css/
│   ├── style.css            # Estilos del sitio para el usuario
│   └── admin_style.css      # Estilos del panel de administración
├── js/
│   ├── script.js
│   └── admin_script.js
├── images/                  # Imágenes propias del template (íconos, banners, etc.)
├── project images/          # Fotos de los productos del catálogo
├── uploaded_img/            # Imágenes subidas por el admin al cargar productos
├── home.php                 # Página principal
├── shop.php                 # Catálogo de productos
├── category.php             # Productos filtrados por categoría
├── search_page.php          # Resultados de búsqueda
├── quick_view.php           # Vista rápida de un producto
├── cart.php                 # Carrito de compras
├── wishlist.php             # Lista de deseos
├── checkout.php             # Finalizar compra
├── orders.php                # Historial de pedidos del usuario
├── about.php / contact.php  # Páginas informativas
├── user_login.php / user_register.php   # Login y registro de usuarios
├── update_user.php          # Edición de datos del usuario
├── shop_db.sql              # Dump de la base de datos
└── README.md
```

## Base de datos

El proyecto usa una base llamada `shop_db` (incluida en `shop_db.sql`) con las siguientes tablas:

- **admins** — usuarios administradores (login del panel)
- **users** — usuarios registrados en la tienda
- **products** — catálogo de productos
- **cart** — productos agregados al carrito por cada usuario
- **wishlist** — productos guardados como favoritos
- **orders** — pedidos realizados
- **messages** — mensajes enviados desde el formulario de contacto

## Instalación y ejecución local

1. **Servidor con PHP y MySQL**: lo más simple es usar XAMPP o WAMP (trae Apache, PHP y MySQL/MariaDB juntos).
2. Copiá la carpeta `ktronix` dentro de `htdocs` (en XAMPP) o la carpeta pública de tu servidor.
3. **Crear la base de datos**: abrí phpMyAdmin, creá una base llamada `shop_db` e importá el archivo `shop_db.sql`.
4. **Configurar la conexión**: revisá `components/connect.php`. Por defecto apunta a:
   ```php
   $db_name = 'mysql:host=localhost;dbname=shop_db';
   $user_name = 'root';
   $user_password = '';
   ```
   Ajustá usuario y contraseña si tu instalación de MySQL los tiene configurados distinto.
5. Iniciá Apache y MySQL desde el panel de XAMPP/WAMP.
6. Entrá desde el navegador a `http://localhost/ktronix/home.php` para el sitio, o `http://localhost/ktronix/admin/admin_login.php` para el panel de administración.

## Usuario administrador por defecto

El dump de la base trae un admin precargado:

- **Usuario:** admin
- **Contraseña:** la que corresponde al hash SHA-1 guardado en la tabla `admins` (conviene cambiarla o crear una cuenta nueva desde `register_admin.php` antes de usarlo en producción).

## Notas

- Las contraseñas se guardan con **SHA-1**, que hoy se considera un algoritmo débil para este fin; si el proyecto se lleva a producción convendría migrar a `password_hash()` de PHP (bcrypt).
- No hay archivo `.env`; la configuración de la base está hardcodeada en `components/connect.php`.
- Las carpetas `images/` y `project images/` son necesarias para que se vean correctamente los banners y las fotos de los productos del catálogo.
