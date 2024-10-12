# 6. Entity Framework

## Definición
Entity Framework (EF) es un marco de trabajo (ORM - Object-Relational Mapper) para .NET que permite a los desarrolladores interactuar con bases de datos utilizando objetos .NET. EF permite la manipulación de datos mediante un modelo de objetos, eliminando la necesidad de escribir mucho código SQL.

## Principales Características
- **Mapeo Objeto-Relacional (ORM)**: Transforma datos entre las bases de datos relacionales y los objetos .NET.
- **Consulta con LINQ**: Permite realizar consultas a la base de datos utilizando LINQ, lo que facilita la lectura y escritura de consultas.
- **Cambio de seguimiento**: Mantiene un seguimiento de los cambios realizados en los objetos y se encarga de generar las sentencias SQL necesarias para persistir esos cambios en la base de datos.
- **Migraciones**: Facilita la gestión de cambios en el esquema de la base de datos a través de migraciones, permitiendo actualizar la estructura sin perder datos.

## Ejemplos de Uso

### 1. **Configuración del Contexto**
Para utilizar EF, primero se debe crear un contexto que herede de `DbContext`.
```csharp
public class MiDbContext : DbContext
{
    public DbSet<Usuario> Usuarios { get; set; }
    public DbSet<Producto> Productos { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Usuario>().ToTable("Usuarios");
        modelBuilder.Entity<Producto>().ToTable("Productos");
    }
}
```

### 2. **Definición de Entidades**
Las entidades son clases que representan las tablas de la base de datos.

```csharp
public class Usuario
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public int Edad { get; set; }
}

public class Producto
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public decimal Precio { get; set; }
}
```

### 3. **Operaciones CRUD**
EF facilita las operaciones de Crear, Leer, Actualizar y Eliminar (CRUD) en la base de datos.

**CREAR**
```csharp
using (var context = new MiDbContext())
{
    var nuevoUsuario = new Usuario { Nombre = "Lucas", Edad = 25 };
    context.Usuarios.Add(nuevoUsuario);
    context.SaveChanges(); // Persiste los cambios en la base de datos
}
```

**LEER**
```csharp
using (var context = new MiDbContext())
{
    var usuarios = context.Usuarios.ToList();
    foreach (var usuario in usuarios)
    {
        Console.WriteLine($"{usuario.Nombre} - {usuario.Edad}");
    }
}
```

**ACTUALIZAR**
```csharp
using (var context = new MiDbContext())
{
    var usuario = context.Usuarios.First(u => u.Nombre == "Lucas");
    usuario.Edad = 31;
    context.SaveChanges(); // Actualiza la base de datos
}
```
**ELIMINAR**
```csharp
using (var context = new MiDbContext())
{
    var usuario = context.Usuarios.First(u => u.Nombre == "Lucas");
    context.Usuarios.Remove(usuario);
    context.SaveChanges(); // Elimina de la base de datos
}
```


Ventajas de Entity Framework
- Desarrollo Rápido: Reduce la cantidad de código necesario para interactuar con bases de datos.
- Modelo de Dominio: Permite trabajar con un modelo de dominio rico, lo que mejora la legibilidad del código.
- Soporte para LINQ: Permite realizar consultas con LINQ, que son más intuitivas y seguras en tiempo de compilación.
- Migraciones: Facilita la evolución del esquema de la base de datos a medida que cambia el modelo de dominio.


Desventajas de Entity Framework
- Rendimiento: En algunos casos, puede ser menos eficiente que escribir consultas SQL optimizadas a mano.
- Curva de Aprendizaje: Puede ser complejo de configurar y usar correctamente, especialmente para proyectos grandes.
- Abstracción: La abstracción puede llevar a una falta de control sobre las consultas generadas y su rendimiento.
--------------------------------

# Métodos de Implementación de Entity Framework

## Introducción
Entity Framework (EF) se puede implementar de varias maneras, dependiendo de las necesidades del proyecto y la estructura de la base de datos. A continuación se describen las metodologías más comunes para implementar EF en aplicaciones .NET.

## 1. **Code First**
### Definición
La metodología **Code First** permite a los desarrolladores definir las clases de entidad en código y luego generar la base de datos a partir de estas clases. Es ideal para proyectos en los que no existe una base de datos existente.

### Pasos para la Implementación
1. **Definir las Clases de Entidad**:
    ```csharp
    public class Producto
    {
        public int Id { get; set; }
        public string Nombre { get; set; }
        public decimal Precio { get; set; }
    }
    ```

2. **Crear el Contexto**:
    ```csharp
    public class MiDbContext : DbContext
    {
        public DbSet<Producto> Productos { get; set; }
    }
    ```

3. **Configurar la Cadena de Conexión** en `appsettings.json`:
    ```json
    {
      "ConnectionStrings": {
          "MiDbContext": "Server=mi_servidor;Database=mi_base_de_datos;User Id=mi_usuario;Password=mi_contraseña;"
      }
    }
    ```

4. **Crear la Base de Datos**:
    - Usar migraciones para crear la base de datos:
      ```bash
      Add-Migration InitialCreate
      Update-Database
      ```

### Ventajas
- Flexibilidad para definir el modelo de datos.
- Posibilidad de evolucionar el esquema a través de migraciones.

### Desventajas
- Puede ser complicado si se trabaja con una base de datos ya existente.

## 2. **Database First**
### Definición
La metodología **Database First** es adecuada para aplicaciones que ya tienen una base de datos existente. Los desarrolladores generan las clases de entidad a partir del esquema de la base de datos.

### Pasos para la Implementación
1. **Crear un Nuevo Proyecto**.
2. **Agregar un Modelo de Datos ADO.NET**.
3. **Seleccionar la Opción "Database First"**.
4. **Conectar a la Base de Datos** y seleccionar las tablas deseadas.
5. **Generar las Clases de Entidad**.

### Ventajas
- Permite trabajar directamente con una base de datos existente.
- Las clases de entidad se generan automáticamente a partir de la estructura de la base de datos.

### Desventajas
- Menos flexibilidad para cambiar el modelo de datos después de que se haya generado.

## 3. **Model First**
### Definición
La metodología **Model First** permite a los desarrolladores crear un modelo visualmente en un diseñador de EF y luego generar tanto el esquema de la base de datos como las clases de entidad a partir de este modelo.

### Pasos para la Implementación
1. **Crear un Diagrama de Modelo** en el Diseñador de Entity Framework.
2. **Definir las Entidades y Relaciones** visualmente.
3. **Generar la Base de Datos** y las Clases de Entidad.

### Ventajas
- Visualización clara del modelo de datos y sus relaciones.
- Generación automática de la base de datos y el código.

### Desventajas
- Puede ser más lento y menos flexible que el enfoque Code First.

## 4. **Dapper (Opcional)**
### Definición
Dapper es un micro ORM que permite a los desarrolladores ejecutar consultas SQL sin la complejidad que a veces acompaña a EF. Si bien no es parte de EF, a menudo se compara con él.

### Uso Básico
```csharp
using (var connection = new SqlConnection(connectionString))
{
    var productos = connection.Query<Producto>("SELECT * FROM Productos").ToList();
}
```

Ventajas
- Rendimiento superior en comparación con EF en ciertas operaciones.
- Menos sobrecarga y control total sobre las consultas SQL.


Desventajas
- Requiere más trabajo manual para manejar el mapeo de datos.

Conclusiones
La elección del método de implementación de Entity Framework depende de las necesidades del proyecto y la arquitectura de la base de datos. Code First es ideal para nuevos proyectos, Database First es adecuado para aplicaciones existentes, y Model First proporciona una interfaz visual para definir el modelo.