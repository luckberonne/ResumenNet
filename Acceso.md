# 13. Modificadores de Acceso en C#

## Definición
Los **modificadores de acceso** en C# son palabras clave que controlan la visibilidad y el acceso a las clases, métodos, propiedades y otros miembros dentro de un programa. Son fundamentales para implementar la encapsulación y la seguridad en el código.

## Tipos de Modificadores de Acceso

### 1. **public**
- **Descripción**: Los miembros declarados como `public` son accesibles desde cualquier otra clase o código en el mismo ensamblado o en otros ensamblados que referencien el ensamblado que contiene la clase.
- **Ejemplo**:
```csharp
public class Usuario
{
    public string Nombre { get; set; }
}

2. private
Descripción: Los miembros declarados como private solo son accesibles dentro de la clase donde están definidos. No se pueden acceder desde ninguna otra clase.
Ejemplo:
csharp
Copiar código
public class Usuario
{
    private string _claveSecreta;

    private void MetodoPrivado()
    {
        // Solo accesible dentro de la clase Usuario
    }
}
3. protected
Descripción: Los miembros declarados como protected son accesibles solo dentro de la clase donde están definidos y en las clases derivadas. Esto permite que las clases que heredan de la clase base accedan a sus miembros.
Ejemplo:
csharp
Copiar código
public class Usuario
{
    protected string Email { get; set; }
}

public class UsuarioPremium : Usuario
{
    public void MostrarEmail()
    {
        Console.WriteLine(Email); // Acceso permitido
    }
}
4. internal
Descripción: Los miembros declarados como internal son accesibles solo dentro del mismo ensamblado (proyecto). No se pueden acceder desde otros ensamblados.
Ejemplo:
csharp
Copiar código
internal class UsuarioInterno
{
    internal void MetodoInterno()
    {
        // Solo accesible dentro del mismo ensamblado
    }
}
5. protected internal
Descripción: Los miembros declarados como protected internal son accesibles desde cualquier lugar dentro del mismo ensamblado y también desde clases derivadas en otros ensamblados.
Ejemplo:
csharp
Copiar código
public class Usuario
{
    protected internal string Nombre { get; set; }
}
Ejemplo de Uso Combinado
Aquí hay un ejemplo que muestra diferentes modificadores de acceso en una clase:

csharp
Copiar código
public class Vehiculo
{
    public string Marca { get; set; }          // Publico
    private int _velocidad;                     // Privado
    protected int _numeroDeRuedas;              // Protegido
    internal string TipoDeCombustible { get; set; } // Interno

    public void Acelerar()
    {
        _velocidad += 10;                       // Acceso a la variable privada
    }
}

public class Coche : Vehiculo
{
    public void MostrarNumeroDeRuedas()
    {
        Console.WriteLine(_numeroDeRuedas);    // Acceso permitido
    }
}
Ventajas de Usar Modificadores de Acceso
Encapsulación: Permiten ocultar detalles de implementación y proteger datos sensibles.
Control de Acceso: Facilitan la implementación de reglas de acceso, asegurando que solo el código adecuado pueda interactuar con ciertos miembros.
Mantenibilidad: Mejora la legibilidad y mantenibilidad del código al definir claramente cómo se puede interactuar con diferentes partes de una clase.
Desventajas de Usar Modificadores de Acceso
Complejidad Adicional: Puede añadir un nivel adicional de complejidad al diseño de clases y a la organización del código.
Rigidez: Si se establecen modificadores de acceso demasiado restrictivos, puede dificultar la reutilización de código en diferentes contextos.