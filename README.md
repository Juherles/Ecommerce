# 🛒 Base de Datos E-commerce

## 📌 Descripción

Este proyecto consiste en el diseño de una base de datos relacional para una aplicación de comercio electrónico (**e-commerce**) utilizando MySQL.

La base de datos está orientada a cubrir las siguientes funcionalidades:

- Creación y autenticación de usuarios.
- Gestión y visualización de un catálogo de productos.
- Carrito de compras asociado a cada usuario.
- Registro de órdenes de compra y seguimiento de pagos.

---

## 🗃️ Estructura de la Base de Datos

La base de datos se llama `ecommerce` y contiene las siguientes tablas:

1. **users**: Almacena los datos de los usuarios registrados.
2. **products**: Catálogo de productos disponibles.
3. **carts**: Carrito de compras por usuario.
4. **cart_items**: Productos agregados a cada carrito.
5. **orders**: Registro de compras realizadas.
6. **order_items**: Detalles de cada producto comprado en una orden.

---

## 📦 Instrucciones SQL

### 1. Crear la base de datos y las tablas

```sql
-- Crear base de datos
CREATE DATABASE IF NOT EXISTS ecommerce;
USE ecommerce;

-- Tabla de usuarios
CREATE TABLE IF NOT EXISTS users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- Tabla de productos
CREATE TABLE IF NOT EXISTS products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock INT DEFAULT 0,
    image_url VARCHAR(255)
);

-- Tabla de carritos
CREATE TABLE IF NOT EXISTS carts (
    cart_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Ítems del carrito
CREATE TABLE IF NOT EXISTS cart_items (
    cart_item_id INT AUTO_INCREMENT PRIMARY KEY,
    cart_id INT,
    product_id INT,
    quantity INT DEFAULT 1,
    FOREIGN KEY (cart_id) REFERENCES carts(cart_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

-- Órdenes
CREATE TABLE IF NOT EXISTS orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    total_amount DECIMAL(10,2),
    payment_status ENUM('pending', 'paid', 'failed') DEFAULT 'pending',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Ítems de las órdenes
CREATE TABLE IF NOT EXISTS order_items (
    order_item_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10,2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```
---

## 2. Insertar datos de prueba

```sql
-- Insertar usuarios
INSERT INTO users (username, email, password_hash) VALUES
('johndoe', 'john@example.com', 'hashpassword1'),
('janedoe', 'jane@example.com', 'hashpassword2'),
('mike123', 'mike@example.com', 'hashpassword3');

-- Insertar productos
INSERT INTO products (name, description, price, stock, image_url) VALUES
('Laptop Gamer', 'Laptop de alto rendimiento para videojuegos.', 1500.00, 10, 'https://example.com/laptop.jpg'),
('Smartphone Pro', 'Teléfono inteligente de última generación.', 999.99, 25, 'https://example.com/smartphone.jpg'),
('Audífonos Inalámbricos', 'Audífonos con cancelación de ruido.', 199.99, 50, 'https://example.com/audifonos.jpg');

-- Insertar carritos
INSERT INTO carts (user_id) VALUES
(1), (2), (3);

-- Agregar productos al carrito
INSERT INTO cart_items (cart_id, product_id, quantity) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 1);

-- Insertar órdenes
INSERT INTO orders (user_id, total_amount, payment_status) VALUES
(1, 1500.00, 'paid'),
(2, 1999.98, 'pending'),
(3, 199.99, 'failed');

-- Detalle de productos comprados
INSERT INTO order_items (order_id, product_id, quantity, price) VALUES
(1, 1, 1, 1500.00),
(2, 2, 2, 999.99),
(3, 3, 1, 199.99);
```
---

## Recursos necesarios

- MySQL Server

- Visual Studio Code

- Extensión SQL (opcional)

- Cliente MySQL (MySQL Workbench, DBeaver, phpMyAdmin)

---

## Estado

✔️ Base de datos funcional
✔️ Datos de prueba insertados
✔️ Listo para conexión con backend en PHP

---

## Autor


---

Puedes pegar este archivo tal cual en Visual Studio Code como `README.md`.  
¿Quieres que te prepare también el `ecommerce_dump.sql` combinando todo?

---