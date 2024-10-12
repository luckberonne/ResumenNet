# 9. Inyección de Dependencias

## Definición
La **inyección de dependencias** (DI) es un patrón de diseño que permite a un objeto recibir sus dependencias desde el exterior en lugar de crearlas por sí mismo. Este enfoque mejora la modularidad y la facilidad de prueba del código, promoviendo un diseño más limpio y desacoplado.

## Principios Fundamentales
- **Inversión de Control (IoC)**: La DI es un tipo de Inversión de Control, donde el flujo de control se invierte al permitir que un objeto gestione sus dependencias.
- **Desacoplamiento**: Facilita la separación de preocupaciones al permitir que las clases se enfoquen en su lógica, dejando la creación de dependencias a un contenedor DI.

## Ejemplo de Inyección de Dependencias en C#

### 1. **Definición de Interfaces y Clases**
Primero, definimos una interfaz y una clase que implementa esa interfaz:

```csharp
public interface IRepositorio
{
    void Agregar(string item);
}

public class Repositorio : IRepositorio
{
    public void Agregar(string item)
    {
        // Lógica para agregar un item
        Console.WriteLine($"Item agregado: {item}");
    }
}
```

### 2. **Clase que Depende de la Interfaz**
Ahora, creamos una clase que depende de IRepositorio:
```csharp
public class Servicio
{
    private readonly IRepositorio _repositorio;

    public Servicio(IRepositorio repositorio)
    {
        _repositorio = repositorio;
    }

    public void Procesar(string item)
    {
        _repositorio.Agregar(item);
    }
}
```

### 3. **Configuración de Inyección de Dependencias**
Usamos un contenedor DI para registrar las dependencias:
```csharp
using Microsoft.Extensions.DependencyInjection;

var serviceProvider = new ServiceCollection()
    .AddTransient<IRepositorio, Repositorio>()
    .AddTransient<Servicio>()
    .BuildServiceProvider();

// Resolviendo el servicio
var servicio = serviceProvider.GetService<Servicio>();
servicio.Procesar("Ejemplo de item");
```

Ventajas de la Inyección de Dependencias
- Facilidad de Pruebas: Permite la creación de pruebas unitarias más fáciles y efectivas, ya que las dependencias pueden ser simuladas (mocked).
- Flexibilidad: Facilita el cambio de implementaciones de dependencias sin modificar el código cliente.
- Mantenibilidad: Mejora la claridad del código y su estructura, lo que hace que sea más fácil de mantener.


Desventajas de la Inyección de Dependencias

- Complejidad: Puede introducir una mayor complejidad, especialmente en aplicaciones pequeñas donde no es necesario un contenedor DI.
- Curva de Aprendizaje: Los desarrolladores nuevos pueden necesitar tiempo para familiarizarse con los conceptos de DI y IoC.
- Contenedores de Inyección de Dependencias Comunes
- Microsoft.Extensions.DependencyInjection: Usado ampliamente en aplicaciones .NET Core.
- Autofac: Un contenedor DI popular que ofrece características avanzadas.
- Ninject: Ofrece una configuración fluida y es fácil de usar.

La inyección de dependencias es una práctica fundamental para construir aplicaciones modulares y mantenibles. 
