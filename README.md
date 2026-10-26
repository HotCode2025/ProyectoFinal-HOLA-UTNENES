# 🌱 RAÍCES LOCALES

> **Conecta con el arte de tu gente**

Proyecto desarrollado por el equipo **HOLA UTNENES**.

---

# 📖 Descripción

**Raíces Locales** es una plataforma ecommerce orientada a la comercialización de productos artesanales de emprendedores locales.

La propuesta busca conectar a los compradores con los creadores de cada producto, ofreciendo no solamente una experiencia de compra sino también la posibilidad de conocer la historia detrás de cada emprendimiento.

Cada producto estará asociado a un artesano o empresa, permitiendo acceder a información sobre su trayectoria, ubicación, especialidad y modalidad de suscripción dentro de la plataforma.

---

# 🎯 Objetivos del Proyecto

- Crear un ecommerce funcional utilizando HTML, CSS y JavaScript.
- Aplicar Programación Orientada a Objetos (POO).
- Utilizar encapsulación mediante clases, getters y setters.
- Implementar un catálogo de productos dinámico.
- Relacionar productos con artesanos.
- Consultar información desde PostgreSQL.
- Implementar un carrito de compras funcional.
- Simular una integración con Mercado Pago.
- Aplicar principios de UI/UX y Responsive Design.

---

# 👥 Equipo HOLA UTNENES

| Integrante | Responsabilidad Principal |
|------------|--------------------------|
| **Otar Kebadze** | Arquitectura e Integración General |
| **Matías Tobares** | Checkout y Mercado Pago |
| **Joaquín** | Modelado de Datos y PostgreSQL |
| **Gabriel** | Catálogo y Productos |
| **Serena** | Vista de Artesanos e Historias |
| **Fernando** | Carrito de Compras |
| **Emmanuel** | UI/UX e Identidad Visual |

---

# 🚀 Alcance de la Primera Versión

## Funcionalidades Operativas

✅ Catálogo de productos

✅ Cards dinámicas

✅ Categorías

✅ Vista detallada de producto

✅ Vista "Conoce al Artesano"

✅ Historias de emprendimientos

✅ Carrito de compras

✅ Persistencia mediante LocalStorage

✅ Checkout

✅ Mercado Pago simulado

✅ Responsive Design

✅ PostgreSQL con datos precargados

---

## Funcionalidades Informativas

### Sistema de Suscripciones

Cada artesano tendrá asociado un tipo de suscripción:

- Básica
- Premium

El sistema estará disponible visualmente pero no podrá contratarse ni modificarse desde la aplicación.

Se utilizará para mostrar el modelo de negocio futuro de la plataforma.

---

### Sistema de Comisiones

La plataforma incluirá una sección informativa donde se explicará el sistema de comisiones sobre ventas.

Las comisiones no afectarán al cálculo del carrito ni al checkout durante esta versión.

---

# 💻 Tecnologías Utilizadas

## Frontend

- HTML5
- CSS3
- JavaScript ES6+

## Base de Datos

- PostgreSQL
- pgAdmin 4

## Persistencia Local

- LocalStorage

## Herramientas

- Git
- GitHub
- Visual Studio Code

## Pasarela de Pago

- Mercado Pago (Simulado)

---

# 🏗 Arquitectura General

La aplicación estará centrada en el frontend utilizando HTML, CSS y JavaScript.

La información será almacenada previamente en PostgreSQL y utilizada por las clases JavaScript del proyecto.

No se desarrollarán funcionalidades de administración de datos desde la interfaz.

Los registros serán cargados manualmente por el equipo para la demostración académica.

---

# 📂 Estructura del Proyecto

```text
RAICES-LOCALES/

├── index.html
├── catalogo.html
├── producto.html
├── artesano.html
├── carrito.html
├── checkout.html
│
├── css/
│   └── styles.css
│
├── js/
│   ├── models/
│   │   ├── Producto.js
│   │   ├── Artesano.js
│   │   └── Carrito.js
│   │
│   ├── services/
│   │   ├── ProductoService.js
│   │   └── ArtesanoService.js
│   │
│   ├── catalogo.js
│   ├── carrito.js
│   ├── checkout.js
│   └── app.js
│
├── database/
│   ├── schema.sql
│   └── inserts.sql
│
├── assets/
│   ├── img/
│   ├── logo/
│   └── icons/
│
└── README.md
```

---

# 🗄 Modelo Relacional

## Relación General

```text
ARTESANO
    │
    │ 1
    │
    ▼
PRODUCTO
    │
    │ N
```

Un artesano puede tener varios productos.

Cada producto pertenece a un único artesano.

---

# 🗃 PostgreSQL 

NOMBRE DE BD: raices_locales_db

## Tabla Artesanos

```sql
CREATE TABLE artesanos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    foto_perfil VARCHAR(255),
    categoria VARCHAR(100),
    ubicacion VARCHAR(100),
    historia TEXT,
    suscripcion VARCHAR(20)
);
```

---

## Tabla Productos

```sql
CREATE TABLE productos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    descripcion TEXT,
    precio DECIMAL(10,2),
    stock INTEGER,
    categoria VARCHAR(100),
    imagen VARCHAR(255),
    destacado BOOLEAN DEFAULT FALSE,

    artesano_id INTEGER,

    CONSTRAINT fk_artesano
    FOREIGN KEY (artesano_id)
    REFERENCES artesanos(id)
);
```

---

# 👨‍🎨 Clase Artesano

```javascript
class Artesano {

  #id;
  #nombre;
  #fotoPerfil;
  #categoria;
  #ubicacion;
  #historia;
  #suscripcion;
  #productos;

  constructor(
    id,
    nombre,
    fotoPerfil,
    categoria,
    ubicacion,
    historia,
    suscripcion,
    productos = []
  ) {
    this.#id = id;
    this.#nombre = nombre;
    this.#fotoPerfil = fotoPerfil;
    this.#categoria = categoria;
    this.#ubicacion = ubicacion;
    this.#historia = historia;
    this.#suscripcion = suscripcion;
    this.#productos = productos;
  }

  getNombre() {}
  getHistoria() {}
  getSuscripcion() {}
  getProductos() {}

  setSuscripcion() {}

  agregarProducto() {}
}
```

---

## Ejemplo de Artesano

```javascript
{
  id: 1,
  nombre: "María Gómez",
  fotoPerfil: "maria.jpg",
  categoria: "Textiles",
  ubicacion: "Mendoza",

  historia:
    "Comencé mi emprendimiento elaborando tejidos artesanales...",

  suscripcion: {
    tipo: "premium",
    activa: true
  },

  productos: []
}
```

---

# 📦 Clase Producto

```javascript
class Producto {

  #id;
  #nombre;
  #descripcion;
  #precio;
  #stock;
  #categoria;
  #imagen;
  #artesanoId;
  #destacado;

  constructor() {}

  getNombre() {}
  getDescripcion() {}
  getPrecio() {}
  getCategoria() {}
  getArtesanoId() {}
  getImagen() {}

  setPrecio() {}
  setStock() {}
}
```

---

## Ejemplo de Producto

```javascript
{
  id: 1,

  nombre: "Manta Andina",

  descripcion:
    "Manta artesanal tejida a mano.",

  precio: 25000,

  stock: 10,

  categoria: "Textiles",

  imagen: "manta.jpg",

  artesanoId: 1,

  destacado: true
}
```

---

# 🛒 Clase Carrito

```javascript
class Carrito {

  #productos = [];

  agregarProducto() {}

  eliminarProducto() {}

  actualizarCantidad() {}

  vaciarCarrito() {}

  calcularTotal() {}

  obtenerProductos() {}
}
```

---

# 📐 Contrato de Clases

## Artesano

### Getters

```javascript
getNombre()
getHistoria()
getSuscripcion()
getProductos()
```

### Métodos

```javascript
setSuscripcion()
agregarProducto()
```

---

## Producto

### Getters

```javascript
getNombre()
getDescripcion()
getPrecio()
getCategoria()
getArtesanoId()
getImagen()
```

### Métodos

```javascript
setPrecio()
setStock()
```

---

## Carrito

### Métodos

```javascript
agregarProducto()

eliminarProducto()

actualizarCantidad()

vaciarCarrito()

calcularTotal()

obtenerProductos()
```

---

# 🖼 Diseño de Card de Producto

**Responsable:** Gabriel

```text
┌────────────────────────┐
│                        │
│        IMAGEN          │
│                        │
├────────────────────────┤
│ Manta Andina           │
│ Textiles               │
│                        │
│ $25.000                │
│                        │
│ ⭐ Premium             │
│                        │
│ Ver Detalle            │
│ Comprar                │
└────────────────────────┘
```

## Información requerida

```javascript
{
  nombre,
  categoria,
  precio,
  imagen,
  destacado
}
```

---

# 👨‍🎨 Vista "Conoce al Artesano"

**Responsable:** Serena

La página obtendrá la información desde PostgreSQL utilizando los objetos del dominio y sus respectivos getters.

## Diseño Conceptual

```text
┌──────────────────────────┐

       FOTO PERFIL

      María Gómez

      📍 Mendoza

      ⭐ Premium

"Comencé mi emprendimiento
en el año 2018 elaborando
tejidos artesanales..."

Productos asociados:

[Manta Andina]
[Bufanda Patagónica]
[Gorro Artesanal]

└──────────────────────────┘
```

## Información requerida

```javascript
{
  nombre,
  fotoPerfil,
  ubicacion,
  historia,
  suscripcion,
  productos
}
```

---

# 🛍 Catálogo

**Responsable:** Gabriel

Funciones:

- Mostrar productos.
- Filtros por categorías.
- Productos destacados.
- Vista detalle.
- Navegación hacia artesanos.

---

# 🛒 Carrito de Compras

**Responsable:** Fernando

Funciones:

- Agregar productos.
- Eliminar productos.
- Modificar cantidades.
- Calcular subtotal.
- Calcular total.
- Guardar carrito en LocalStorage.

---

# 💳 Checkout y Mercado Pago

**Responsable:** Matías Tobares

Mercado Pago será implementado como simulación.

Estados posibles:

- ✅ Pago aprobado
- ⏳ Pago pendiente
- ❌ Pago rechazado

No se realizarán transacciones económicas reales.

---

# 🧩 Integración General

**Responsable:** Otar Kebadze

Funciones:

- Integración de módulos.
- Control de calidad.
- Revisión de estructura.
- Testing general.
- Organización del repositorio.
- Entrega final.

---

# 🎨 UI / UX

**Responsable:** Emmanuel

Funciones:

- Diseño general.
- Sistema visual.
- Responsive Design.
- Logo.
- Paleta de colores.

---

# 🎨 Paleta de Colores Oficial

## Verde Principal

```css
#2E7D32
```

Uso:
- Botones principales.
- Acciones positivas.
- Navegación.

---

## Terracota

```css
#C65D3B
```

Uso:
- Destacados.
- CTA secundarios.

---

## Crema

```css
#F8F5F0
```

Uso:
- Fondo principal.

---

## Gris Oscuro

```css
#333333
```

Uso:
- Texto principal.

---

## Dorado Premium

```css
#D4AF37
```

Uso:
- Distintivos Premium.
- Productos destacados.
- Suscripciones Premium.

---

## Variables CSS

```css
:root {

  --primary: #2E7D32;
  --secondary: #C65D3B;
  --background: #F8F5F0;
  --dark: #333333;
  --premium: #D4AF37;
  --white: #FFFFFF;

}
```

---

# 🔮 Funcionalidades Futuras

- Integración real con Mercado Pago.
- Gestión completa de suscripciones.
- Estadísticas de ventas.
- Sistema de valoraciones.
- Publicación dinámica de productos.

---

# ✅ Distribución Final de Tareas

### Otar Kebadze
Integración y Coordinación Técnica, testing y entrega.

### Matías Tobares
Checkout y simulación de Mercado Pago.

### Joaquín
PostgreSQL, modelado de datos, clases, getters, setters y relaciones.

### Gabriel
Catálogo, cards, filtros y detalle de productos.

### Serena
Historias, perfiles y vista "Conoce al Artesano".

### Fernando
Carrito de compras y LocalStorage.

### Emmanuel
UI/UX, identidad visual, branding y responsive design.

---

# 📌 Conclusión

**Raíces Locales** busca acercar a los usuarios a los emprendedores detrás de cada producto artesanal, combinando comercio electrónico con historias reales y una identidad visual centrada en la producción local.

La primera versión del proyecto aplica Programación Orientada a Objetos, PostgreSQL, encapsulación mediante getters y setters, relaciones entre entidades, gestión de estado en frontend y simulación de procesos comerciales reales, manteniendo un alcance adecuado para el contexto académico y dejando preparada la base para futuras ampliaciones.
