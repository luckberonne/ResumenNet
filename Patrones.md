# 7. Patrones de Diseño

## Definición
Los patrones de diseño son soluciones reutilizables a problemas comunes en el desarrollo de software. Proporcionan una forma de estructurar y organizar el código, mejorando la legibilidad, la mantenibilidad y la escalabilidad de las aplicaciones.

## Clasificación de Patrones de Diseño
Los patrones de diseño se dividen en tres categorías principales:

### 1. **Patrones Creacionales**
Estos patrones se centran en la creación de objetos de manera que se ajusten a la situación de uso.

- **Ejemplos:**
  - **Singleton**: Garantiza que una clase tenga una única instancia y proporciona un punto de acceso global a ella.
    ```csharp
    public class Singleton
    {
        private static Singleton _instance;
        private static readonly object _lock = new object();

        private Singleton() { }

        public static Singleton Instance
        {
            get
            {
                lock (_lock)
                {
                    return _instance ??= new Singleton();
                }
            }
        }
    }
    ```

  - **Factory Method**: Define una interfaz para crear un objeto, pero permite que las subclases decidan qué clase instanciar.
    ```csharp
    public abstract class Creator
    {
        public abstract Producto FactoryMethod();
    }

    public class ConcreteCreator : Creator
    {
        public override Producto FactoryMethod()
        {
            return new ProductoConcreto();
        }
    }
    ```

### 2. **Patrones Estructurales**
Estos patrones se centran en la composición de clases y objetos para formar estructuras más grandes.

- **Ejemplos:**
  - **Adapter**: Permite que clases con interfaces incompatibles trabajen juntas.
    ```csharp
    public interface ITarget
    {
        string Request();
    }

    public class Adaptee
    {
        public string SpecificRequest()
        {
            return "Hola desde Adaptee";
        }
    }

    public class Adapter : ITarget
    {
        private Adaptee _adaptee = new Adaptee();

        public string Request()
        {
            return _adaptee.SpecificRequest();
        }
    }
    ```

  - **Composite**: Permite tratar objetos individuales y compuestos de manera uniforme.
    ```csharp
    public interface IComponent
    {
        void Operation();
    }

    public class Leaf : IComponent
    {
        public void Operation()
        {
            // Operación de hoja
        }
    }

    public class Composite : IComponent
    {
        private List<IComponent> _children = new List<IComponent>();

        public void Add(IComponent component)
        {
            _children.Add(component);
        }

        public void Operation()
        {
            foreach (var child in _children)
            {
                child.Operation();
            }
        }
    }
    ```

### 3. **Patrones de Comportamiento**
Estos patrones se centran en cómo los objetos interactúan y se comunican entre sí.

- **Ejemplos:**
  - **Observer**: Define una relación de dependencia uno a muchos entre objetos, de modo que cuando un objeto cambie su estado, todos sus dependientes sean notificados y actualizados automáticamente.
    ```csharp
    public interface IObserver
    {
        void Update();
    }

    public class Subject
    {
        private List<IObserver> _observers = new List<IObserver>();

        public void Attach(IObserver observer)
        {
            _observers.Add(observer);
        }

        public void Notify()
        {
            foreach (var observer in _observers)
            {
                observer.Update();
            }
        }
    }
    ```

  - **Strategy**: Permite definir una familia de algoritmos, encapsular cada uno y hacerlos intercambiables.
    ```csharp
    public interface IStrategy
    {
        void Execute();
    }

    public class ConcreteStrategyA : IStrategy
    {
        public void Execute()
        {
            // Algoritmo A
        }
    }

    public class Context
    {
        private IStrategy _strategy;

        public void SetStrategy(IStrategy strategy)
        {
            _strategy = strategy;
        }

        public void ExecuteStrategy()
        {
            _strategy.Execute();
        }
    }
    ```

## Ventajas de los Patrones de Diseño
- **Reutilización de Código**: Facilitan la reutilización de soluciones probadas.
- **Mejor Mantenibilidad**: Facilitan la modificación y la extensión del código.
- **Facilitan la Comunicación**: Proporcionan un vocabulario común para discutir problemas y soluciones en el desarrollo de software.

## Desventajas de los Patrones de Diseño
- **Complejidad**: La implementación de patrones puede añadir complejidad innecesaria si no se aplica correctamente.
- **Sobrecarga**: Algunos patrones pueden introducir sobrecarga en el rendimiento debido a su estructura abstracta.

---

Los patrones de diseño son herramientas valiosas que pueden mejorar la calidad del software y la colaboración en equipo. Si deseas profundizar en algún patrón específico o necesitas más ejemplos, ¡házmelo saber!
