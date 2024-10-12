# 12. API y sus Verbos

## Definición
Una **API (Interfaz de Programación de Aplicaciones)** es un conjunto de reglas y protocolos que permiten a diferentes aplicaciones comunicarse entre sí. En el contexto de aplicaciones web, una API REST (Transferencia de Estado Representacional) se utiliza comúnmente para permitir que los clientes interactúen con el servidor utilizando HTTP.

## Principios de las API REST
- **Sin estado**: Cada solicitud del cliente al servidor debe contener toda la información necesaria para entender y procesar la solicitud.
- **Recursos**: Las APIs REST se centran en la manipulación de recursos, que son representaciones de datos en la aplicación.
- **Usar HTTP**: Las APIs REST utilizan los métodos HTTP para realizar operaciones sobre los recursos.

## Verbos HTTP Comunes

### 1. **GET**
- **Descripción**: Se utiliza para recuperar datos de un servidor.
- **Ejemplo**: Obtener una lista de usuarios.
```http
GET /api/usuarios
2. POST
Descripción: Se utiliza para enviar datos al servidor, a menudo para crear un nuevo recurso.
Ejemplo: Crear un nuevo usuario.
http
Copiar código
POST /api/usuarios
{
    "nombre": "Lucas",
    "email": "lucas@example.com"
}
3. PUT
Descripción: Se utiliza para actualizar un recurso existente en su totalidad.
Ejemplo: Actualizar la información de un usuario existente.
http
Copiar código
PUT /api/usuarios/1
{
    "nombre": "Lucas Ariel",
    "email": "lucas.ariel@example.com"
}
4. PATCH
Descripción: Se utiliza para realizar una actualización parcial en un recurso existente.
Ejemplo: Actualizar solo el email de un usuario.
http
Copiar código
PATCH /api/usuarios/1
{
    "email": "nuevoemail@example.com"
}
5. DELETE
Descripción: Se utiliza para eliminar un recurso del servidor.
Ejemplo: Eliminar un usuario existente.
http
Copiar código
DELETE /api/usuarios/1
Ejemplo de Implementación de una API en ASP.NET Core
1. Definición del Controlador
Aquí tienes un ejemplo simple de un controlador de API en ASP.NET Core:

csharp
Copiar código
[ApiController]
[Route("api/[controller]")]
public class UsuariosController : ControllerBase
{
    private readonly IRepositorio _repositorio;

    public UsuariosController(IRepositorio repositorio)
    {
        _repositorio = repositorio;
    }

    [HttpGet]
    public IActionResult GetUsuarios()
    {
        var usuarios = _repositorio.GetUsuarios();
        return Ok(usuarios);
    }

    [HttpPost]
    public IActionResult CrearUsuario([FromBody] UsuarioDto usuarioDto)
    {
        _repositorio.Agregar(usuarioDto);
        return CreatedAtAction(nameof(GetUsuarios), new { id = usuarioDto.Id }, usuarioDto);
    }

    // Métodos para PUT, PATCH y DELETE...
}
Ventajas de Utilizar APIs
Interoperabilidad: Permite que diferentes aplicaciones y servicios se comuniquen entre sí.
Escalabilidad: Facilita el crecimiento de la aplicación, ya que diferentes componentes pueden escalar de manera independiente.
Mantenibilidad: Mejora la capacidad de mantenimiento al permitir que diferentes partes de una aplicación se desarrollen y desplieguen de manera independiente.
Desventajas de Utilizar APIs
Complejidad: Puede agregar complejidad al sistema, especialmente si no se gestionan adecuadamente las versiones de la API.
Latencia: Las llamadas a la API pueden introducir latencia en la comunicación entre el cliente y el servidor.
