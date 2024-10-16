Patrones de Diseño de Software
Los patrones de diseño de software son soluciones reutilizables y probadas a problemas comunes en el desarrollo de software. Estos patrones no son código específico, sino guías o plantillas que se pueden adaptar a diversos contextos. Los patrones de diseño ayudan a mejorar la mantenibilidad, escalabilidad, y robustez del software.

A continuación, se describen los principales tipos de patrones de diseño, junto con algunos ejemplos:

1. Patrones Creacionales
Estos patrones se centran en cómo se crean los objetos. Mejoran la flexibilidad y reutilización del código al abstraer la lógica de creación de instancias.

Factory Method: Define una interfaz para crear un objeto, pero permite a las subclases decidir qué clase instanciar.

Ejemplo:

csharp
Copiar código
// Interfaz del producto
public interface IProducto { void Operacion(); }

// Producto concreto
public class ProductoA : IProducto { public void Operacion() { Console.WriteLine("Producto A"); } }

// Fábrica abstracta
public abstract class Creador
{
    public abstract IProducto CrearProducto();
}

// Fábrica concreta
public class CreadorConcreto : Creador
{
    public override IProducto CrearProducto() { return new ProductoA(); }
}
Singleton: Garantiza que una clase tenga solo una instancia y proporciona un punto de acceso global a esa instancia.

Ejemplo:

csharp
Copiar código
public class Singleton
{
    private static Singleton _instance;

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new Singleton();
            }
            return _instance;
        }
    }
}
Builder: Separa la construcción de un objeto complejo de su representación, permitiendo crear diferentes representaciones del objeto.

Ejemplo:

csharp
Copiar código
public class Producto
{
    public string ParteA { get; set; }
    public string ParteB { get; set; }
}

public class ProductoBuilder
{
    private Producto _producto = new Producto();

    public ProductoBuilder SetParteA(string parteA)
    {
        _producto.ParteA = parteA;
        return this;
    }

    public ProductoBuilder SetParteB(string parteB)
    {
        _producto.ParteB = parteB;
        return this;
    }

    public Producto Build() => _producto;
}
2. Patrones Estructurales
Estos patrones se ocupan de la composición de clases y objetos para formar estructuras más grandes y complejas.

Adapter: Convierte la interfaz de una clase en otra interfaz que el cliente espera. Permite que clases con interfaces incompatibles trabajen juntas.

Ejemplo:

csharp
Copiar código
public interface IEnchufeEuropeo { void Conectar(); }
public class EnchufeAmericano { public void ConectarAmericano() { Console.WriteLine("Conectado a enchufe americano"); } }

public class Adaptador : IEnchufeEuropeo
{
    private EnchufeAmericano _enchufeAmericano;
    
    public Adaptador(EnchufeAmericano enchufeAmericano)
    {
        _enchufeAmericano = enchufeAmericano;
    }

    public void Conectar()
    {
        _enchufeAmericano.ConectarAmericano();
    }
}
Composite: Permite tratar objetos individuales y grupos de objetos de manera uniforme. Es útil para representar jerarquías de objetos.

Ejemplo:

csharp
Copiar código
public interface IComponente
{
    void Mostrar();
}

public class Hoja : IComponente
{
    public void Mostrar() { Console.WriteLine("Hoja"); }
}

public class Compuesto : IComponente
{
    private List<IComponente> _componentes = new List<IComponente>();

    public void Agregar(IComponente componente) { _componentes.Add(componente); }

    public void Mostrar()
    {
        foreach (var componente in _componentes)
        {
            componente.Mostrar();
        }
    }
}
Facade: Proporciona una interfaz simplificada a un sistema complejo de clases, librerías, o frameworks.

Ejemplo:

csharp
Copiar código
public class Subsistema1 { public void Operacion1() { Console.WriteLine("Operación 1"); } }
public class Subsistema2 { public void Operacion2() { Console.WriteLine("Operación 2"); } }

public class Fachada
{
    private Subsistema1 _subsistema1 = new Subsistema1();
    private Subsistema2 _subsistema2 = new Subsistema2();

    public void OperacionSimplificada()
    {
        _subsistema1.Operacion1();
        _subsistema2.Operacion2();
    }
}
3. Patrones de Comportamiento
Estos patrones se centran en la interacción entre objetos y cómo se comunican entre ellos.

Observer: Define una dependencia uno a muchos, donde un cambio en el estado de un objeto notifica y actualiza automáticamente a todos sus dependientes (observadores).

Ejemplo:

csharp
Copiar código
public class Sujeto
{
    private List<IObservador> _observadores = new List<IObservador>();

    public void AgregarObservador(IObservador observador) { _observadores.Add(observador); }

    public void Notificar()
    {
        foreach (var observador in _observadores)
        {
            observador.Actualizar();
        }
    }
}

public interface IObservador
{
    void Actualizar();
}

public class ObservadorConcreto : IObservador
{
    public void Actualizar() { Console.WriteLine("Observador actualizado"); }
}
Strategy: Permite definir una familia de algoritmos, encapsular cada uno de ellos y hacerlos intercambiables. El algoritmo que se use puede variar sin cambiar el contexto que lo usa.

Ejemplo:

csharp
Copiar código
public interface IStrategy { void Ejecutar(); }

public class EstrategiaA : IStrategy { public void Ejecutar() { Console.WriteLine("Estrategia A ejecutada"); } }

public class Contexto
{
    private IStrategy _estrategia;

    public void SetEstrategia(IStrategy estrategia) { _estrategia = estrategia; }

    public void EjecutarEstrategia() { _estrategia.Ejecutar(); }
}
Command: Encapsula una solicitud como un objeto, permitiendo parametrizar clientes con diferentes solicitudes, poner en cola solicitudes o registrar operaciones.

Ejemplo:

csharp
Copiar código
public interface ICommand
{
    void Ejecutar();
}

public class ComandoConcreto : ICommand
{
    public void Ejecutar() { Console.WriteLine("Comando ejecutado"); }
}

public class Invocador
{
    private ICommand _comando;

    public void SetComando(ICommand comando) { _comando = comando; }

    public void EjecutarComando() { _comando.Ejecutar(); }
}
Conclusión
Los patrones de diseño son herramientas poderosas que permiten resolver problemas comunes en el desarrollo de software de una manera eficiente, reutilizable y mantenible. Dependiendo del contexto, uno o varios patrones pueden aplicarse para mejorar la estructura y flexibilidad del código.






