# 14. Delegados y Eventos

## Definición
- **Delegados**: Son tipos de referencia que permiten encapsular un método. Un delegado puede apuntar a un método que coincide con su firma, permitiendo así la invocación de ese método de manera indirecta.
- **Eventos**: Son un mecanismo que permite a una clase o a un objeto notificar la ocurrencia de un evento a los suscriptores. Se basan en delegados para gestionar la invocación de los métodos suscritos.

## Delegados

### 1. **Ejemplo de Delegado**
```csharp
public delegate void NotificarCambio(string mensaje);

public class Proceso
{
    public event NotificarCambio CambioOcurrido;

    public void Ejecutar()
    {
        // Lógica del proceso
        CambioOcurrido?.Invoke("El proceso ha sido ejecutado.");
    }
}
2. Uso de Delegados
Los delegados permiten crear métodos que pueden ser pasados como parámetros, lo que facilita la creación de métodos de orden superior.

csharp
Copiar código
public class Calculadora
{
    public delegate int Operacion(int a, int b);

    public int EjecutarOperacion(int a, int b, Operacion operacion)
    {
        return operacion(a, b);
    }
}
Eventos
1. Declaración de Eventos
Los eventos se declaran utilizando un delegado. A continuación, se muestra cómo declarar un evento en una clase:

csharp
Copiar código
public class Temporizador
{
    public event EventHandler TiempoFuera;

    public void Iniciar(int segundos)
    {
        Task.Delay(segundos * 1000).ContinueWith(t => OnTiempoFuera());
    }

    protected virtual void OnTiempoFuera()
    {
        TiempoFuera?.Invoke(this, EventArgs.Empty);
    }
}
2. Suscribirse a Eventos
Los consumidores pueden suscribirse a eventos para recibir notificaciones:

csharp
Copiar código
public class Programa
{
    public static void Main()
    {
        var temporizador = new Temporizador();
        temporizador.TiempoFuera += (sender, e) => Console.WriteLine("El tiempo ha terminado.");
        temporizador.Iniciar(5);
    }
}
Ventajas de Usar Delegados y Eventos
Desacoplamiento: Permiten un diseño más desacoplado, ya que los productores de eventos no necesitan conocer los detalles de los consumidores.
Flexibilidad: Facilitan la implementación de patrones como el Observador, donde un objeto puede notificar a otros sobre cambios de estado.
Manejadores de Eventos: Habilitan la programación orientada a eventos, lo que es útil en aplicaciones GUI y sistemas de notificación.
Desventajas de Usar Delegados y Eventos
Complejidad: Puede añadir complejidad al código, especialmente si se usan en exceso o de manera incorrecta.
Fugas de Memoria: Si no se desuscriben adecuadamente de los eventos, pueden provocar fugas de memoria debido a referencias mantenidas entre los objetos.
