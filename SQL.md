# 15. SQL Server

## Definición
**SQL Server** es un sistema de gestión de bases de datos relacional (RDBMS) desarrollado por Microsoft. Proporciona herramientas y servicios para almacenar, gestionar y analizar datos, permitiendo a las aplicaciones acceder a la información de manera eficiente.

## Características Principales

### 1. **Transacciones**
SQL Server admite transacciones, lo que garantiza la atomicidad, consistencia, aislamiento y durabilidad (ACID). Esto significa que las operaciones dentro de una transacción se completan completamente o no se completan en absoluto.

- **Ejemplo de Transacción**:
```sql
BEGIN TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 100
WHERE Id = 1;

UPDATE Cuenta
SET Saldo = Saldo + 100
WHERE Id = 2;

COMMIT; -- O ROLLBACK en caso de error
2. Índices
Los índices son estructuras de datos que mejoran la velocidad de recuperación de datos en una tabla. Pueden ser índices únicos, compuestos o de texto completo.

Ejemplo de Creación de un Índice:
sql
Copiar código
CREATE INDEX idx_nombre ON Clientes(Nombre);
3. Procedimientos Almacenados
Los procedimientos almacenados son conjuntos de instrucciones SQL que se almacenan en la base de datos y pueden ser ejecutados de manera eficiente. Son útiles para encapsular lógica de negocio.

Ejemplo de Procedimiento Almacenado:
sql
Copiar código
CREATE PROCEDURE ObtenerClientesActivos
AS
BEGIN
    SELECT * FROM Clientes WHERE Activo = 1;
END;
4. Funciones
Las funciones son similares a los procedimientos almacenados, pero pueden devolver un valor y pueden ser utilizadas en consultas.

Ejemplo de Función:
sql
Copiar código
CREATE FUNCTION ObtenerTotalVentas(@ClienteId INT)
RETURNS DECIMAL
AS
BEGIN
    DECLARE @Total DECIMAL;
    SELECT @Total = SUM(Monto) FROM Ventas WHERE ClienteId = @ClienteId;
    RETURN @Total;
END;
5. Vistas
Las vistas son consultas almacenadas que pueden ser tratadas como tablas. Proporcionan una capa de abstracción y simplifican la seguridad al restringir el acceso a ciertas columnas y filas.

Ejemplo de Creación de una Vista:
sql
Copiar código
CREATE VIEW VistaClientesActivos AS
SELECT Nombre, Email FROM Clientes WHERE Activo = 1;
6. Seguridad
SQL Server ofrece un robusto modelo de seguridad que incluye autenticación, autorización y roles. Los permisos pueden ser asignados a usuarios o roles para controlar el acceso a los objetos de la base de datos.

Ejemplo de Asignación de Permisos:
sql
Copiar código
GRANT SELECT ON dbo.Clientes TO UsuarioEjemplo;
Ventajas de Usar SQL Server
Rendimiento: Optimizado para operaciones de consulta y manejo de grandes volúmenes de datos.
Integración: Se integra fácilmente con otras herramientas de Microsoft, como Power BI y Excel.
Características Avanzadas: Soporta características como particionamiento de tablas, replicación y análisis de datos.
Desventajas de Usar SQL Server
Costo: Puede ser costoso en comparación con algunas alternativas de código abierto.
Recursos: Requiere más recursos del sistema en comparación con algunas bases de datos ligeras.


# 16. Claves Foráneas y Restricciones en SQL Server

## Definición
Las **claves foráneas** son columnas en una tabla que crean una relación entre esa tabla y otra. Se utilizan para garantizar la integridad referencial entre tablas, asegurando que los valores en una columna coincidan con los valores de otra tabla.

## Claves Foráneas

### 1. **Creación de Claves Foráneas**
Una clave foránea establece una relación entre dos tablas. Por ejemplo, una tabla de `Pedidos` puede tener una clave foránea que se refiere a la tabla de `Clientes`.

- **Ejemplo de Creación de una Clave Foránea**:
```sql
CREATE TABLE Clientes (
    Id INT PRIMARY KEY,
    Nombre NVARCHAR(100)
);

CREATE TABLE Pedidos (
    Id INT PRIMARY KEY,
    ClienteId INT,
    FechaPedido DATETIME,
    FOREIGN KEY (ClienteId) REFERENCES Clientes(Id)
);
2. Comportamiento de las Claves Foráneas
Las claves foráneas pueden tener comportamientos específicos al actualizar o eliminar registros en la tabla referenciada:

CASCADE: Propagar cambios (actualizaciones o eliminaciones) a las tablas dependientes.

SET NULL: Establecer la clave foránea en NULL cuando se elimina o actualiza el registro referenciado.

NO ACTION: No permite la eliminación o actualización si existen registros relacionados.

Ejemplo de Clave Foránea con Comportamiento CASCADE:

sql
Copiar código
CREATE TABLE Pedidos (
    Id INT PRIMARY KEY,
    ClienteId INT,
    FechaPedido DATETIME,
    FOREIGN KEY (ClienteId) REFERENCES Clientes(Id) ON DELETE CASCADE
);
Restricciones
1. Restricciones de Clave Primaria
Una clave primaria es una restricción que identifica de manera única cada fila en una tabla. No puede contener valores NULL y debe ser única.

Ejemplo de Clave Primaria:
sql
Copiar código
CREATE TABLE Productos (
    Id INT PRIMARY KEY,
    Nombre NVARCHAR(100) NOT NULL
);
2. Restricciones NOT NULL
Esta restricción se utiliza para especificar que una columna no puede contener valores NULL.

Ejemplo de Restricción NOT NULL:
sql
Copiar código
CREATE TABLE Usuarios (
    Id INT PRIMARY KEY,
    Nombre NVARCHAR(100) NOT NULL,
    Email NVARCHAR(100) NOT NULL
);
3. Restricciones UNIQUE
Aseguran que todos los valores en una columna sean únicos. Se puede aplicar a una o más columnas.

Ejemplo de Restricción UNIQUE:
sql
Copiar código
CREATE TABLE Clientes (
    Id INT PRIMARY KEY,
    Email NVARCHAR(100) UNIQUE
);
4. Restricciones CHECK
Se utilizan para limitar los valores que se pueden insertar en una columna, asegurando que cumplen con una condición específica.

Ejemplo de Restricción CHECK:
sql
Copiar código
CREATE TABLE Productos (
    Id INT PRIMARY KEY,
    Precio DECIMAL(10, 2),
    CHECK (Precio > 0)
);
5. Restricciones DEFAULT
Se utilizan para asignar un valor predeterminado a una columna cuando no se proporciona un valor al insertar un nuevo registro.

Ejemplo de Restricción DEFAULT:
sql
Copiar código
CREATE TABLE Usuarios (
    Id INT PRIMARY KEY,
    FechaRegistro DATETIME DEFAULT GETDATE()
);
Ventajas de Usar Claves Foráneas y Restricciones
Integridad Referencial: Garantiza que los datos relacionados sean coherentes y válidos.
Validación de Datos: Las restricciones ayudan a mantener la calidad y precisión de los datos al validar las entradas.
Facilitación de Relaciones: Simplifican el manejo de relaciones entre tablas, lo que mejora la estructura de la base de datos.
Desventajas de Usar Claves Foráneas y Restricciones
Rendimiento: Pueden afectar el rendimiento de las operaciones de inserción y actualización, ya que se deben validar las relaciones.
Complejidad en Diseño: Un diseño complejo de relaciones puede dificultar la comprensión de la estructura de la base de datos.