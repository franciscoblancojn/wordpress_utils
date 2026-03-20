# wordpress_utils

[![PHP Version](https://img.shields.io/badge/PHP-%3E%3D7.4-blue.svg)](https://php.net/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Packagist](https://img.shields.io/packagist/v/franciscoblancojn/wordpress_utils.svg)](https://packagist.org/packages/franciscoblancojn/wordpress_utils)

Una librería PHP moderna para WordPress que ofrece utilidades reutilizables, comenzando con un sistema de logs dinámico y extensible.

---

## 🚀 Características

- ✅ Sistema de logs dinámico por clave (`key`)
- ✅ Persistencia usando `get_option` / `update_option`
- ✅ Interfaz visual en el panel de administración de WordPress
- ✅ Soporte para múltiples logs independientes
- ✅ Fácil integración con plugins existentes
- ✅ Compatible con Composer (PSR-4)

---

## 📦 Instalación

### Vía Composer

```bash
composer require franciscoblancojn/wordpress_utils
```

---

## ⚡ Inicio Rápido

### 1. Cargar Composer en tu plugin

```php
require_once __DIR__ . '/vendor/autoload.php';
```

### 2. Inicializar el sistema de logs

```php
use franciscoblancojn\wordpress_utils\FWUSystemLog;

FWUSystemLog::init("MY_PLUGIN_SLUG");
```

### 3. Agregar logs

```php
FWUSystemLog::add("MY_PLUGIN_SLUG", [
    "type"    => "API",
    "message" => "Solicitud enviada correctamente",
    "data"    => ["id" => 123]
]);
```

### 4. Ver logs en WordPress

Una vez inicializado, aparecerá una nueva opción en el menú del administrador:

> 👉 **MY_PLUGIN_SLUG_LOG**

Desde esta página podrás **ver**, **copiar** y **limpiar** los logs registrados.

---

## 🧠 Conceptos

### 🔑 Clave (`key`)

Cada log funciona de forma completamente independiente usando una clave única:

```php
FWUSystemLog::init("PAYMENTS");
FWUSystemLog::init("ORDERS");
```

### 🗂️ Tipos de log

Los logs se agrupan automáticamente por el campo `type`:

```php
FWUSystemLog::add("MY_PLUGIN_SLUG", [
    "type"    => "ERROR",
    "message" => "Falló conexión"
]);
```

---

## ⚙️ Configuración opcional

Puedes personalizar el comportamiento definiendo constantes antes de llamar a `init()`:

| Constante | Tipo | Descripción |
|---|---|---|
| `MY_PLUGIN_SLUG_LOG` | `bool` | Activa o desactiva el sistema de logs |
| `MY_PLUGIN_SLUG_LOG_COUNT` | `int` | Cantidad máxima de registros por tipo |
| `MY_PLUGIN_SLUG_LOG_KEY` | `string` | Clave personalizada para almacenamiento en la DB |

```php
define("MY_PLUGIN_SLUG_LOG",       true);          // activar/desactivar logs
define("MY_PLUGIN_SLUG_LOG_COUNT", 50);            // cantidad máxima por tipo
define("MY_PLUGIN_SLUG_LOG_KEY",   "custom_key");  // clave en la DB
```

---

## 🧪 Ejemplo completo

```php
use franciscoblancojn\wordpress_utils\FWUSystemLog;

// Inicializar
FWUSystemLog::init("MY_PLUGIN");

// Agregar log
FWUSystemLog::add("MY_PLUGIN", [
    "type"    => "DEBUG",
    "message" => "Plugin cargado",
    "data"    => ["user" => get_current_user_id()]
]);
```

---

## ⚠️ Requisitos

- PHP >= 7.4
- WordPress (usa funciones como `get_option`, `add_action`, etc.)
- Composer (recomendado)

---

## 💡 Notas

- La librería **solo funciona dentro de WordPress**
- Los logs se almacenan en la tabla `wp_options`
- Pensado para **debugging y monitoreo interno** de plugins

---

## 📝 Licencia

Este proyecto está bajo la licencia [MIT](LICENSE). Eres libre de usarlo, modificarlo y distribuirlo.

---

## 👨‍💻 Autor

**Francisco Blanco**  
🔗 [franciscoblanco.vercel.app](https://franciscoblanco.vercel.app/)