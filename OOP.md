# 3. Programación Orientada a Objetos (OOP)

## Definición
La Programación Orientada a Objetos (OOP) es un paradigma de programación que utiliza "objetos" para representar datos y métodos que operan sobre esos datos. OOP se basa en varios principios que promueven la encapsulación, la reutilización del código y la modularidad.

## Principios Clave de OOP

### 1. **Encapsulamiento**
- **Definición**: Agrupa datos y comportamientos en una única entidad (clase) y restringe el acceso a algunos de los componentes. Esto se logra utilizando modificadores de acceso como `private`, `protected`, y `public`.
- **Ejemplo**:
    ```csharp
    public class CuentaBancaria
    {
        private decimal saldo;

        public void Depositar(decimal cantidad)
        {
            if (cantidad > 0)
            {
                saldo += cantidad;
            }
        }

        public decimal ObtenerSaldo()
        {
            return saldo;
        }
    }
    ```
  En este ejemplo, `saldo` está encapsulado dentro de la clase `CuentaBancaria`, y solo puede ser modificado mediante el método `Depositar`.

### 2. **Herencia**
- **Definición**: Permite que una clase (clase derivada) herede propiedades y métodos de otra clase (clase base). Esto promueve la reutilización del código.
- **Ejemplo**:
    ```csharp
    public class Vehiculo
    {
        public int NumeroRuedas { get; set; }
    }

    public class Coche : Vehiculo
    {
        public string Marca { get; set; }
    }
    ```
  Aquí, la clase `Coche` hereda de `Vehiculo`, lo que significa que puede acceder a la propiedad `NumeroRuedas`.

### 3. **Polimorfismo**
- **Definición**: Permite que una variable, función o método adopte diferentes formas. En OOP, esto se logra a través de la sobrecarga de métodos y la implementación de interfaces.
- **Ejemplo**:
    ```csharp
    public class Animal
    {
        public virtual void HacerSonido()
        {
            Console.WriteLine("Sonido de animal");
        }
    }

    public class Perro : Animal
    {
        public override void HacerSonido()
        {
            Console.WriteLine("Guau");
        }
    }

    public class Gato : Animal
    {
        public override void HacerSonido()
        {
            Console.WriteLine("Miau");
        }
    }
    ```
  En este ejemplo, `HacerSonido` se comporta de manera diferente según el tipo de objeto que lo invoque (perro o gato).

### 4. **Abstracción**
- **Definición**: Permite ocultar detalles de implementación y mostrar solo las características relevantes de un objeto. Esto se logra mediante clases abstractas y interfaces.
- **Ejemplo**:
    ```csharp
    public abstract class Forma
    {
        public abstract double CalcularArea();
    }

    public class Circulo : Forma
    {
        public double Radio { get; set; }
        public override double CalcularArea() => Math.PI * Radio * Radio;
    }
    ```
  Aquí, la clase `Forma` define un método abstracto `CalcularArea` que debe ser implementado por cualquier clase que herede de ella.

## Ventajas de OOP
- **Modularidad**: El código se organiza en clases, lo que facilita la gestión y el mantenimiento.
- **Reutilización**: Facilita la reutilización del código mediante herencia y polimorfismo.
- **Flexibilidad**: Permite adaptar y extender el software de manera más sencilla.

## Desventajas de OOP
- **Complejidad**: La OOP puede ser más compleja de implementar y entender en comparación con otros paradigmas, especialmente para principiantes.
- **Rendimiento**: Puede haber una ligera sobrecarga de rendimiento debido a la creación de objetos y la gestión de memoria.
- **Diseño Inicial**: Requiere un diseño cuidadoso y planificación para asegurar que los objetos y relaciones sean correctamente definidos.

---

La Programación Orientada a Objetos es fundamental en el desarrollo de software moderno y es ampliamente utilizada en .NET. Si tienes preguntas sobre algún principio específico o deseas profundizar en otro tema, ¡hazmelo saber!
