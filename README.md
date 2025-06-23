# 🛠️ Taller MySQL

TALLER DE MYSQL
Normalización
DIAGRAMA 
![alt text](image-1.png)


Creación de las tablas en la terminal de MYSQL
CREATE TABLE contactoProveedores (
    id INT AUTO_INCREMENT PRIMARY KEY,
    proveedor_id INT,
    nombre_contacto VARCHAR(100),
    telefono VARCHAR(20),
    email VARCHAR(100),
    FOREIGN KEY (proveedor_id) REFERENCES proveedores(id)
);
CREATE TABLE tipoProductos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    tipo_nombre VARCHAR(100),
    description TEXT
);

CREATE TABLE EmpleadoProveedor (
    empleado_id INT,
    proveedor_id INT,
    PRIMARY KEY (empleado_id, proveedor_id),
    FOREIGN KEY (empleado_id) REFERENCES datosEmpleados(id),
    FOREIGN KEY (proveedor_id) REFERENCES proveedores(id)
);
CREATE TABLE datosEmpleados (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    puesto_id INT,
    salario DECIMAL(10, 2),
    fecha_contratacion DATE,
    FOREIGN KEY (puesto_id) REFERENCES puestos(id)
);
CREATE TABLE telefonos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    numero VARCHAR(20),
    tipo VARCHAR(20),
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    empleado_id INT,
    fecha DATE,
    total DECIMAL(10, 2),
    cliente_id INT,
    FOREIGN KEY (empleado_id)REFERENCES datosempleados(id),
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

ALTER TABLE historialPedidos
ADD FOREIGN KEY (pedido_id) REFERENCES pedidos(id);

CREATE TABLE ubicaciones(  id INT AUTO_INCREMENT PRIMARY REY, 
 direccion VARCHAR(255),
 ciudad VARCHAR(100),
 codigo_postal VARCHAR(10),
estado VARCHAR(50),
pais VARCHAR(50) 
); 
CREATE TABLE clientes(
    id INT AUTO_INCREMENT PRIMARY KEY, 
    nombre VARCHAR(100), 
    email VARCHAR(100) UNIQUE, 
    ubicacion_id INT, 
    FOREIGN KEY (ubicacion_id) REFERENCES ubicaciones(id)
    );

CREATE TABLE proveedores(
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    ubicacion_id INT,
    FOREIGN KEY (ubicacion_id)REFERENCES ubicaciones(id)
);
CREATE TABLE productos(
    id INT AUTO_INCREMENT PRIMARY KEY,
    proveedor_id INT,
    nombre_contacto VARCHAR(100),
    telefono VARCHAR(20),
    email VARCHAR(100),
    tipo_id INT,
    precio DECIMAL(10, 2),
    FOREIGN KEY (tipo_id)REFERENCES tipoproductos(id),
    FOREIGN KEY (proveedor_id)REFERENCES proveedores(id)
);
CREATE TABLE detallePedido(
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    producto_id INT,
    cantidad INT,
    precio DECIMAL(10, 2),
    FOREIGN KEY (pedido_id)REFERENCES pedidos(id),
    FOREIGN KEY (producto_id)REFERENCES productos(id)
);
CREATE TABLE puestos(
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50) UNIQUE
);
CREATE TABLE historialPedidos(
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    estado_anterior VARCHAR(50),
    estado_nuevo VARCHAR(50),
    fecha_cambio DATETIME,
    usuario VARCHAR(100)
);

Comandos DML
INSERT INTO clientes(nombre, email, ubicacion_id) VALUES('camilo','corzogmail.com',2),( 'jose' ,'jose@gmail.com',     NULL ),('carlos gomez','carlos@gmail.com', 1),('maria duarte', 'maria@gmail.com',1);
INSERT INTO clientes(id, nombre, email, ubicacion_id) VALUES (200, 'luis martinez','luis@gmail.com',100);
INSERT INTO datosempleados(nombre, puesto_id, salario, fecha_contratacion) VALUES ('gerente', 1, 1230000, '2025-06-22'),('ana lopez', 1,2200,2, '2023-05-10'),('andres ruiz', 1, 2500,2024-01-10);
INSERT INTO clientes(id, nombre,puesto_id, salario,fecha_contratacion) VALUES (300, 'andrea rojas', 1, 2800,'2024-05-01');
INSERT INTO detallepedido(id,pedido_id,producto_id,cantidad,precio)VALUES (6,1,1,2,1500),(7,1,2,5,25.000),(8,1,3,3,40000),(9,1,4,1,200000),(10,1,5,10,10000);  
INSERT INTO pedidos (id, empleado_id, fecha, total, cliente_id) VALUES(1, 300, '2025-06-22', 2000.00, 200),(2, 1, '2025-06-22', 4.00, NULL),(3, 1, '2025-06-24', 4.00, NULL),(4, NULL, '2025-06-22', 150.00, 1),(5, NULL, '2025-06-01', 120.00, 1),(6, NULL, '2025-06-05', 80.00, 1),(7, NULL, '2025-06-10', 200.00, 1),(8, 1, '2025-06-22', 120.00, 1),(9, 1, '2025-06-22', 250.00, 1),
INSERT INTO productos ( proveedor_id, nombre_contacto, telefono, email, tipo_id, precio) VALUES( 1, 'jabon', '3214088506', 'juanpP@gmail.com', NULL, 500.00),( 1, 'escoba', '3001234567', 'luis@mail.com', 1, 300.00),( 1, 'trapero', '3001234567', 'producto1@mail.com', 1, 250.00),( 1, 'recogedor', '3001234567', 'producto2@mail.com', 1, NULL),( 1, 'jabon de ropa', '3001234567', 'producto3@mail.com', 1, NULL),( 1, 'jabon de loza', '3001234567', 'producto4@mail.com', 1, NULL),( 1, 'jabon en polvo', '3001234567', 'producto5@mail.com', 1, NULL),( 1, 'servilleta', '1234567890', 'laptopx@mail.com', 1, 1500.00),( 1, 'papel', '1234567890', 'mouse@mail.com', 1, 25.00),( 1, 'jabon liquido', '1234567890', 'teclado@mail.com', 1, 40.00),( 1, 'shampoo', '1234567890', 'monitor@mail.com', 1, 200.00),( 1, 'jabon para el cuerpo', '1234567890', 'usb@mail.com', 1, 10.00);
INSERT INTO proveedores(noombre,ubicacion_id)VALUES ('edwin camilo corzo sanchez',100);
INSERT INTO puestos(nombre) VALUES('administrador');
INSERT INTO tipoproductos(tipo_nombre, description) VALUES ('aseo','utiles para una mejor higiene'),('electrica','productos electronicos');
INSERT INTO ubicaciones (id, direccion, ciudad, codigo_postal, estado, pais) VALUES(1, 'carrera23#4', 'piedecuesta', '21323', 'santander', 'colombia'),(2, 'Calle Falsa 123', 'Bogotá', '110111', 'Cundinamarca', 'Colombia'),(3, 'Calle 10', 'Piedecuesta', '681011', 'Santander', 'Colombia'),(4, 'Calle 10', 'Piedecuesta', '681011', 'Santander', 'Colombia'),(100, 'Calle 20 #5-30', 'Piedecuesta', '681011', 'Santander', 'Colombia');


Joins
1. Obtener la lista de todos los pedidos con los nombres de clientes usando INNER JOIN . 
 SELECT p.id AS pedido_id, c.nombre AS cliente, p.fecha, p.total
    FROM pedidos p
    INNER JOIN clientes c ON p.cliente_id = c.id;
+-----------+---------------+------------+---------+
| pedido_id | cliente       | fecha      | total   |
+-----------+---------------+------------+---------+
|         4 | camilo        | 2025-06-22 |  150.00 |
|         5 | camilo        | 2025-06-01 |  120.00 |
|         6 | camilo        | 2025-06-05 |   80.00 |
|         7 | camilo        | 2025-06-10 |  200.00 |
|         8 | camilo        | 2025-06-22 |  120.00 |
|         9 | camilo        | 2025-06-22 |  250.00 |
|         1 | Luis Martínez | 2025-06-22 | 2000.00 |
|       400 | Luis Martínez | 2025-06-22 |  150.00 |
+-----------+---------------+------------+---------+

2. Listar los productos y proveedores que los suministran con INNER JOIN .
 SELECT pr.id AS producto_id, pr.nombre_contacto AS producto, prov.nombre AS proveedor
 FROM productos pr
 INNER JOIN proveedores prov ON pr.proveedor_id = prov.id;
+-------------+----------------------+----------------------------+
| producto_id | producto             | proveedor                  |
+-------------+----------------------+----------------------------+
|           1 | jabon                | Edwin Camilo Corzo Sanchez |
|           2 | escoba               | Edwin Camilo Corzo Sanchez |
|           3 | trapero              | Edwin Camilo Corzo Sanchez |
|           4 | recogedor            | Edwin Camilo Corzo Sanchez |
|           5 | jabon de ropa        | Edwin Camilo Corzo Sanchez |
|           6 | jabon de loza        | Edwin Camilo Corzo Sanchez |
|           7 | jabon en polvo       | Edwin Camilo Corzo Sanchez |
|           8 | servilleta           | Edwin Camilo Corzo Sanchez |
|           9 | papel                | Edwin Camilo Corzo Sanchez |
|          10 | jabon liquido        | Edwin Camilo Corzo Sanchez |
|          11 | shampoo              | Edwin Camilo Corzo Sanchez |
|          12 | jabon para el cuerpo | Edwin Camilo Corzo Sanchez |
+-------------+----------------------+----------------------------+
12 rows in set (0.01 sec)


3. Mostrar los pedidos y las ubicaciones de los clientes con LEFT JOIN . 
SELECT p.id AS pedido_id, c.nombre AS cliente, u.ciudad
    FROM pedidos p
    LEFT JOIN clientes c ON p.cliente_id = c.id
    LEFT JOIN ubicaciones u ON c.ubicacion_id = u.id;
+-----------+---------------+-------------+
| pedido_id | cliente       | ciudad      |
+-----------+---------------+-------------+
|         2 | NULL          | NULL        |
|         3 | NULL          | NULL        |
|         4 | camilo        | Bogotá      |
|         5 | camilo        | Bogotá      |
|         6 | camilo        | Bogotá      |
|         7 | camilo        | Bogotá      |
|         8 | camilo        | Bogotá      |
|         9 | camilo        | Bogotá      |
|         1 | Luis Martínez | Piedecuesta |
|       400 | Luis Martínez | Piedecuesta |
+-----------+---------------+-------------+
4. Consultar los empleados que han registrado pedidos, incluyendo empleados sin pedidos ( LEFT JOIN ).
 SELECT e.id AS empleado_id, e.nombre AS empleado, p.id AS pedido_id
    FROM datosempleados e
    LEFT JOIN pedidos p ON e.id = p.empleado_id;
+-------------+--------------+-----------+
| empleado_id | empleado     | pedido_id |
+-------------+--------------+-----------+
|           1 | gerente      |         2 |
|           1 | gerente      |         3 |
|           1 | gerente      |         8 |
|           1 | gerente      |         9 |
|           2 | Ana López    |      NULL |
|           3 | Andrés Ruiz  |      NULL |
|         300 | Andrea Rojas |         1 |
|         300 | Andrea Rojas |       400 |
+-------------+--------------+-----------+

5. Obtener el tipo de producto y los productos asociados con INNER JOIN . 
 SELECT tp.id AS tipo_id, tp.tipo_nombre, pr.nombre_contacto AS producto
    FROM tipoproductos tp
    INNER JOIN productos pr ON pr.tipo_id = tp.id;
+---------+-------------+----------------------+
| tipo_id | tipo_nombre | producto             |
+---------+-------------+----------------------+
|       1 | aseo        | escoba               |
|       1 | aseo        | trapero              |
|       1 | aseo        | recogedor            |
|       1 | aseo        | jabon de ropa        |
|       1 | aseo        | jabon de loza        |
|       1 | aseo        | jabon en polvo       |
|       1 | aseo        | servilleta           |
|       1 | aseo        | papel                |
|       1 | aseo        | jabon liquido        |
|       1 | aseo        | shampoo              |
|       1 | aseo        | jabon para el cuerpo |
+---------+-------------+----------------------+
6. Listar todos los clientes y el número de pedidos realizados con COUNT y GROUP BY .	
 SELECT c.id AS cliente_id, c.nombre AS cliente, COUNT(p.id) AS total_pedidos
    FROM clientes c
    LEFT JOIN pedidos p ON c.id = p.cliente_id
    GROUP BY c.id, c.nombre;
+------------+---------------+---------------+
| cliente_id | cliente       | total_pedidos |
+------------+---------------+---------------+
|          1 | camilo        |             6 |
|          2 | jose          |             0 |
|          3 | Carlos Gómez  |             0 |
|          4 | María Duarte  |             0 |
|        200 | Luis Martínez |             2 |
+------------+---------------+---------------+


7. Combinar Pedidos y Empleados para mostrar qué empleados gestionaron pedidos específicos. 
 SELECT p.id AS pedido_id, e.id AS empleado_id, e.nombre AS empleado
    FROM pedidos p
    INNER JOIN datosempleados e ON p.empleado_id = e.id;
+-----------+-------------+--------------+
| pedido_id | empleado_id | empleado     |
+-----------+-------------+--------------+
|         2 |           1 | gerente      |
|         3 |           1 | gerente      |
|         8 |           1 | gerente      |
|         9 |           1 | gerente      |
|         1 |         300 | Andrea Rojas |
|       400 |         300 | Andrea Rojas |
+-----------+-------------+--------------+
8. Mostrar productos que no han sido pedidos ( RIGHT JOIN ).
SELECT pr.id AS producto_id, pr.nombre_contacto AS producto
    FROM detallepedido dp
    RIGHT JOIN productos pr ON pr.id = dp.producto_id
    WHERE dp.id IS NULL;
+-------------+----------------------+
| producto_id | producto             |
+-------------+----------------------+
|           6 | jabon de loza        |
|           7 | jabon en polvo       |
|           8 | servilleta           |
|           9 | papel                |
|          10 | jabon liquido        |
|          11 | shampoo              |
|          12 | jabon para el cuerpo |
+-------------+----------------------+

9. Mostrar el total de pedidos y ubicación de clientes usando múltiples JOIN .
SELECT c.id AS cliente_id, c.nombre AS cliente, u.ciudad, COUNT(p.id) AS total_pedidos
    FROM clientes c
    LEFT JOIN pedidos p ON c.id = p.cliente_id
    LEFT JOIN ubicaciones u ON c.ubicacion_id = u.id
    GROUP BY c.id, c.nombre, u.ciudad;
+------------+---------------+-------------+---------------+
| cliente_id | cliente       | ciudad      | total_pedidos |
+------------+---------------+-------------+---------------+
|          1 | camilo        | Bogotá      |             6 |
|          2 | jose          | NULL        |             0 |
|          3 | Carlos Gómez  | piedecuesta |             0 |
|          4 | María Duarte  | piedecuesta |             0 |
|        200 | Luis Martínez | Piedecuesta |             2 |
+------------+---------------+-------------+---------------+ 

10. Unir Proveedores , Productos , y TiposProductos para un listado completo de inventario.
 SELECT prov.id AS proveedor_id, prov.nombre AS proveedor, pr.nombre_contacto AS producto, tp.tipo_nombre
    FROM proveedores prov
    INNER JOIN productos pr ON pr.proveedor_id = prov.id
    INNER JOIN tipoproductos tp ON pr.tipo_id = tp.id;
+--------------+----------------------------+----------------------+-------------+
| proveedor_id | proveedor                  | producto             | tipo_nombre |
+--------------+----------------------------+----------------------+-------------+
|            1 | Edwin Camilo Corzo Sanchez | escoba               | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | trapero              | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | recogedor            | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | jabon de ropa        | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | jabon de loza        | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | jabon en polvo       | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | servilleta           | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | papel                | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | jabon liquido        | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | shampoo              | aseo        |
|            1 | Edwin Camilo Corzo Sanchez | jabon para el cuerpo | aseo        |
+--------------+----------------------------+----------------------+-------------+

3. Consultas Simples 
1. Seleccionar todos los productos con precio mayor a $50. 
 SELECT id, nombre_contacto AS producto, precio
    FROM productos
    WHERE precio > 50;
+----+------------+---------+
| id | producto   | precio  |
+----+------------+---------+
|  1 | jabon      |  500.00 |
|  2 | escoba     |  300.00 |
|  3 | trapero    |  250.00 |
|  8 | servilleta | 1500.00 |
| 11 | shampoo    |  200.00 |
+----+------------+---------+
2. Consultar clientes registrados en una ciudad específica.
SELECT c.id, c.nombre, u.ciudad
    FROM clientes c
    INNER JOIN ubicaciones u ON c.ubicacion_id = u.id
    WHERE u.ciudad = 'Bogotá';
+----+--------+--------+
| id | nombre | ciudad |
+----+--------+--------+
|  1 | camilo | Bogotá |
+----+--------+--------+

3. Mostrar empleados contratados en los últimos 2 años.
 SELECT id, nombre, fecha_contratacion
    FROM datosempleados
    WHERE fecha_contratacion >= DATE_SUB(CURDATE(), INTERVAL 2 YEAR);
+-----+--------------+--------------------+
| id  | nombre       | fecha_contratacion |
+-----+--------------+--------------------+
|   1 | gerente      | 2025-06-22         |
|   3 | Andrés Ruiz  | 2024-01-10         |
| 300 | Andrea Rojas | 2024-05-01         |
+-----+--------------+--------------------+ 
4. Seleccionar proveedores que suministran más de 5 productos
 SELECT prov.id, prov.nombre, COUNT(pr.id) AS total_productos
    FROM proveedores prov
    INNER JOIN productos pr ON prov.id = pr.proveedor_id
    GROUP BY prov.id, prov.nombre
    HAVING COUNT(pr.id) > 5;
+----+----------------------------+-----------------+
| id | nombre                     | total_productos |
+----+----------------------------+-----------------+
|  1 | Edwin Camilo Corzo Sanchez |              12 |
+----+----------------------------+-----------------+

5. Listar clientes que no tienen dirección registrada en UbicacionCliente . 6. Calcular el total de ventas por cada cliente.
SELECT id, nombre, email
    FROM clientes
    WHERE ubicacion_id IS NULL;
+----+--------+----------------+
| id | nombre | email          |
+----+--------+----------------+
|  2 | jose   | jose@gmail.com |
+----+--------+----------------+
6. Calcular el total de ventas por cada cliente.
 SELECT c.id AS cliente_id, c.nombre, SUM(p.total) AS total_ventas
    FROM clientes c
    INNER JOIN pedidos p ON c.id = p.cliente_id
    GROUP BY c.id, c.nombre;
+------------+---------------+--------------+
| cliente_id | nombre        | total_ventas |
+------------+---------------+--------------+
|        200 | Luis Martínez |      2150.00 |
|          1 | camilo        |       920.00 |
+------------+---------------+--------------+
7. Mostrar el salario promedio de los empleados. 
 SELECT AVG(salario) AS salario_promedio
    FROM datosempleados;
+------------------+
| salario_promedio |
+------------------+
|    309375.000000 |
+------------------+
8. Consultar el tipo de productos disponibles en TiposProductos .
SELECT id, tipo_nombre, description
    FROM tipoproductos;
+----+-------------+-------------------------------+
| id | tipo_nombre | description                   |
+----+-------------+-------------------------------+
|  1 | aseo        | utiles para una mejor higiene |
|  2 | Electrónica | Productos electrónicos        |
+----+-------------+-------------------------------+

9. Seleccionar los 3 productos más caros. 
SELECT id, nombre_contacto AS producto, precio
    FROM productos
    ORDER BY precio DESC
    LIMIT 3;
+----+------------+---------+
| id | producto   | precio  |
+----+------------+---------+
|  8 | servilleta | 1500.00 |
|  1 | jabon      |  500.00 |
|  2 | escoba     |  300.00 |

10. Consultar el cliente con el mayor número de pedidos.
SELECT c.id, c.nombre, COUNT(p.id) AS total_pedidos
    FROM clientes c
    INNER JOIN pedidos p ON c.id = p.cliente_id
    GROUP BY c.id, c.nombre
    ORDER BY total_pedidos DESC
    LIMIT 1;
+----+--------+---------------+
| id | nombre | total_pedidos |
+----+--------+---------------+
|  1 | camilo |             6 |
+----+--------+---------------+
4. Consultas Multitabla 
1. Listar todos los pedidos y el cliente asociado.
SELECT p.id AS pedido_id, c.nombre AS cliente, p.fecha, p.total
    FROM pedidos p
    INNER JOIN clientes c ON p.cliente_id = c.id;
+-----------+---------------+------------+---------+
| pedido_id | cliente       | fecha      | total   |
+-----------+---------------+------------+---------+
|         4 | camilo        | 2025-06-22 |  150.00 |
|         5 | camilo        | 2025-06-01 |  120.00 |
|         6 | camilo        | 2025-06-05 |   80.00 |
|         7 | camilo        | 2025-06-10 |  200.00 |
|         8 | camilo        | 2025-06-22 |  120.00 |
|         9 | camilo        | 2025-06-22 |  250.00 |
|         1 | Luis Martínez | 2025-06-22 | 2000.00 |
|       400 | Luis Martínez | 2025-06-22 |  150.00 |
+-----------+---------------+------------+---------+ 
2. Mostrar la ubicación de cada cliente en sus pedidos.
 SELECT p.id AS pedido_id, c.nombre AS cliente, u.ciudad
    FROM pedidos p
    INNER JOIN clientes c ON p.cliente_id = c.id
    INNER JOIN ubicaciones u ON c.ubicacion_id = u.id;
+-----------+---------------+-------------+
| pedido_id | cliente       | ciudad      |
+-----------+---------------+-------------+
|         4 | camilo        | Bogotá      |
|         5 | camilo        | Bogotá      |
|         6 | camilo        | Bogotá      |
|         7 | camilo        | Bogotá      |
|         8 | camilo        | Bogotá      |
|         9 | camilo        | Bogotá      |
|         1 | Luis Martínez | Piedecuesta |
|       400 | Luis Martínez | Piedecuesta |
+-----------+---------------+-------------+

3. Listar productos junto con el proveedor y tipo de producto.
 SELECT pr.id, pr.nombre_contacto AS producto, prov.nombre AS proveedor, tp.tipo_nombre
    FROM productos pr
    INNER JOIN proveedores prov ON pr.proveedor_id = prov.id
    INNER JOIN tipoproductos tp ON pr.tipo_id = tp.id;
+----+----------------------+----------------------------+-------------+
| id | producto             | proveedor                  | tipo_nombre |
+----+----------------------+----------------------------+-------------+
|  2 | escoba               | Edwin Camilo Corzo Sanchez | aseo        |
|  3 | trapero              | Edwin Camilo Corzo Sanchez | aseo        |
|  4 | recogedor            | Edwin Camilo Corzo Sanchez | aseo        |
|  5 | jabon de ropa        | Edwin Camilo Corzo Sanchez | aseo        |
|  6 | jabon de loza        | Edwin Camilo Corzo Sanchez | aseo        |
|  7 | jabon en polvo       | Edwin Camilo Corzo Sanchez | aseo        |
|  8 | servilleta           | Edwin Camilo Corzo Sanchez | aseo        |
|  9 | papel                | Edwin Camilo Corzo Sanchez | aseo        |
| 10 | jabon liquido        | Edwin Camilo Corzo Sanchez | aseo        |
| 11 | shampoo              | Edwin Camilo Corzo Sanchez | aseo        |
| 12 | jabon para el cuerpo | Edwin Camilo Corzo Sanchez | aseo        |
+----+----------------------+----------------------------+-------------+
4. Consultar todos los empleados que gestionan pedidos de clientes en una ciudad específica.
SELECT e.id AS empleado_id, e.nombre AS empleado, u.ciudad
    FROM datosempleados e
    JOIN pedidos p ON e.id = p.empleado_id
    JOIN clientes c ON p.cliente_id = c.id
    JOIN ubicaciones u ON c.ubicacion_id = u.id
    WHERE u.ciudad = 'Piedecuesta';
+-------------+--------------+-------------+
| empleado_id | empleado     | ciudad      |
+-------------+--------------+-------------+
|         300 | Andrea Rojas | Piedecuesta |
|         300 | Andrea Rojas | Piedecuesta |
+-------------+--------------+-------------+

5. Consultar los 5 productos más vendidos. 
 SELECT pr.id, pr.nombre_contacto AS producto, SUM(dp.cantidad) AS total_vendidos
    FROM productos pr
    JOIN detallepedido dp ON pr.id = dp.producto_id
    GROUP BY pr.id, pr.nombre_contacto
    ORDER BY total_vendidos DESC
    LIMIT 5;
+----+---------------+----------------+
| id | producto      | total_vendidos |
+----+---------------+----------------+
|  5 | jabon de ropa |             10 |
|  2 | escoba        |              5 |
|  3 | trapero       |              3 |
|  1 | jabon         |              2 |
|  4 | recogedor     |              1 |
+----+---------------+----------------+
6. Obtener la cantidad total de pedidos por cliente y ciudad
 SELECT c.id, c.nombre, u.ciudad, COUNT(p.id) AS total_pedidos
    FROM clientes c
    LEFT JOIN pedidos p ON c.id = p.cliente_id
    LEFT JOIN ubicaciones u ON c.ubicacion_id = u.id
    GROUP BY c.id, c.nombre, u.ciudad;
+-----+---------------+-------------+---------------+
| id  | nombre        | ciudad      | total_pedidos |
+-----+---------------+-------------+---------------+
|   1 | camilo        | Bogotá      |             6 |
|   2 | jose          | NULL        |             0 |
|   3 | Carlos Gómez  | piedecuesta |             0 |
|   4 | María Duarte  | piedecuesta |             0 |
| 200 | Luis Martínez | Piedecuesta |             2 |
+-----+---------------+-------------+---------------+

7. Listar clientes y proveedores en la misma ciudad.
 SELECT c.id AS cliente_id, c.nombre AS cliente, p.id AS proveedor_id, p.nombre AS proveedor, u.ciudad
     FROM clientes c
     JOIN ubicaciones u ON c.ubicacion_id = u.id
     JOIN proveedores p ON p.ubicacion_id = u.id;
+------------+---------------+--------------+----------------------------+-------------+
| cliente_id | cliente       | proveedor_id | proveedor                  | ciudad      |
+------------+---------------+--------------+----------------------------+-------------+
|        200 | Luis Martínez |            1 | Edwin Camilo Corzo Sanchez | Piedecuesta |
+------------+---------------+--------------+----------------------------+-------------+
8. Mostrar el total de ventas agrupado por tipo de producto.
SELECT tp.tipo_nombre, SUM(dp.cantidad * dp.precio) AS total_ventas
    FROM detallepedido dp
    JOIN productos pr ON dp.producto_id = pr.id
    JOIN tipoproductos tp ON pr.tipo_id = tp.id
    GROUP BY tp.tipo_nombre;
+-------------+--------------+
| tipo_nombre | total_ventas |
+-------------+--------------+
| aseo        |       545.00 |
+-------------+--------------+


9. Listar empleados que gestionan pedidos de productos de un proveedor específico. 
 SELECT DISTINCT e.id, e.nombre
    FROM datosempleados e
    JOIN pedidos p ON e.id = p.empleado_id
    JOIN detallepedido dp ON p.id = dp.pedido_id
    JOIN productos pr ON dp.producto_id = pr.id
    WHERE pr.proveedor_id = 1;
+-----+--------------+
| id  | nombre       |
+-----+--------------+
| 300 | Andrea Rojas |
+-----+--------------+
10. Obtener el ingreso total de cada proveedor a partir de los productos vendidos
SELECT prov.id, prov.nombre, SUM(dp.cantidad * dp.precio) AS ingreso_total
    FROM proveedores prov
    JOIN productos pr ON prov.id = pr.proveedor_id
    JOIN detallepedido dp ON pr.id = dp.producto_id
    GROUP BY prov.id, prov.nombre;
+----+----------------------------+---------------+
| id | nombre                     | ingreso_total |
+----+----------------------------+---------------+
|  1 | Edwin Camilo Corzo Sanchez |       3545.00 |
+----+----------------------------+---------------+

ENLACE DE UN DRIVE CON UN WORD PARA UNA FORMA VISUAL 
https://drive.google.com/drive/folders/1r_ZoKEnTAABYrYaI-1LOXMolVWzYbFmB?usp=sharing

INGRESAR AL README PARA MEJOR VISUALIZACION DESDE EL REPOSITORIO NO SE VE BIEN
https://github.com/Edwincamilocorzosanchez/TALLER_MYSQL.git