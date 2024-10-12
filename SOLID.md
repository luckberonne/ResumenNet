# 2. SOLID

## Definición
SOLID es un acrónimo que representa cinco principios de diseño orientado a objetos que ayudan a los desarrolladores a crear software más comprensible, flexible y mantenible. Estos principios son fundamentales para mejorar la calidad del código y facilitar su evolución a lo largo del tiempo.

## Principios SOLID

### 1. **Single Responsibility Principle (SRP)**
- **Definición**: Una clase debe tener una única razón para cambiar, lo que significa que debe tener una única responsabilidad.
- **Ejemplo**: 
    ```csharp
    public class ReportGenerator
    {
        public void GenerateReport() { /* Generar informe */ }
    }

    public class ReportSaver
    {
        public void SaveReport() { /* Guardar informe */ }
    }
    ```
  En este ejemplo, la generación y el guardado del informe se separan en dos clases, cada una con una responsabilidad única.

### 2. **Open/Closed Principle (OCP)**
- **Definición**: Las clases deben estar abiertas para la extensión, pero cerradas para la modificación. Esto significa que se deben poder agregar nuevas funcionalidades sin cambiar el código existente.
- **Ejemplo**:
    ```csharp
    public abstract class Shape
    {
        public abstract double Area();
    }

    public class Circle : Shape
    {
        public double Radius { get; set; }
        public override double Area() => Math.PI * Radius * Radius;
    }

    public class Square : Shape
    {
        public double Side { get; set; }
        public override double Area() => Side * Side;
    }
    ```
  Nuevas formas pueden ser agregadas sin modificar las clases existentes.

### 3. **Liskov Substitution Principle (LSP)**
- **Definición**: Los objetos de una clase derivada deben poder reemplazar a los objetos de la clase base sin alterar el funcionamiento del programa.
- **Ejemplo**:
    ```csharp
    public class Bird
    {
        public virtual void Fly() { /* Volar */ }
    }

    public class Sparrow : Bird { /* Implementación específica */ }

    public class Ostrich : Bird
    {
        public override void Fly() => throw new NotImplementedException();
    }
    ```
  En este caso, `Ostrich` no puede ser sustituido donde se espera que `Bird` vuele, violando el LSP.

### 4. **Interface Segregation Principle (ISP)**
- **Definición**: Es mejor tener varias interfaces específicas en lugar de una interfaz general. Esto evita que las clases dependan de métodos que no utilizan.
- **Ejemplo**:
    ```csharp
    public interface IPrinter
    {
        void Print();
    }

    public interface IScanner
    {
        void Scan();
    }

    public class MultiFunctionPrinter : IPrinter, IScanner
    {
        public void Print() { /* Imprimir */ }
        public void Scan() { /* Escanear */ }
    }
    ```
  Aquí, `MultiFunctionPrinter` implementa solo las interfaces necesarias, evitando un diseño en el que un dispositivo de impresión no puede escanear.

### 5. **Dependency Inversion Principle (DIP)**
- **Definición**: Las dependencias deben ser abstraídas. Las clases de alto nivel no deben depender de clases de bajo nivel, ambas deben depender de abstracciones (interfaces).
- **Ejemplo**:
    ```csharp
    public interface IMessageSender
    {
        void Send(string message);
    }

    public class EmailSender : IMessageSender
    {
        public void Send(string message) { /* Enviar correo */ }
    }

    public class Notification
    {
        private readonly IMessageSender _messageSender;

        public Notification(IMessageSender messageSender)
        {
            _messageSender = messageSender;
        }

        public void Notify(string message) => _messageSender.Send(message);
    }
    ```
  En este ejemplo, `Notification` depende de la abstracción `IMessageSender`, lo que permite cambiar el mecanismo de envío sin modificar la clase `Notification`.

## Ventajas de SOLID
- **Mantenibilidad**: Facilita la modificación y el mantenimiento del código.
- **Reutilización**: Promueve la reutilización de código a través de clases e interfaces bien definidas.
- **Flexibilidad**: Permite adaptaciones y cambios en el software sin afectar otras partes del sistema.

## Desventajas de SOLID
- **Complejidad Inicial**: Implementar todos los principios SOLID puede aumentar la complejidad del diseño inicial.
- **Sobrecarga de Interfaces**: Un exceso de interfaces puede dificultar la comprensión del código.
- **Requiere Disciplina**: Seguir estos principios requiere una buena práctica y disciplina, lo que puede ser un desafío en proyectos apresurados.

---

Los principios SOLID son esenciales para el desarrollo de software de alta calidad en .NET y en otros lenguajes de programación. Si tienes preguntas sobre algún principio específico o deseas profundizar en otro tema, ¡dímelo!
