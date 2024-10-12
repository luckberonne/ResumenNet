# 11. Mapper

## Definición
El **mapeo de objetos** (Mapper) se refiere a la técnica utilizada para convertir un objeto de un tipo a otro, comúnmente de un objeto de dominio a un objeto de transferencia de datos (DTO) o viceversa. Esta técnica es fundamental en aplicaciones donde los datos deben ser transmitidos a través de capas, como la capa de presentación y la capa de acceso a datos.

## Importancia del Mapeo
- **Desacoplamiento**: Permite separar las capas de la aplicación, lo que mejora la mantenibilidad y la legibilidad del código.
- **Eficiencia**: Facilita la transferencia de datos entre diferentes capas y reduce el riesgo de exposición de detalles internos del modelo de dominio.
- **Conversión de Datos**: Permite adaptar los datos a las necesidades específicas de la capa que los utiliza, evitando la sobrecarga de transportar objetos complejos innecesariamente.

## Ejemplo de Mapeo Manual

### 1. **Definición de Clases**
Supongamos que tenemos una clase de dominio y una clase DTO:

```csharp
public class Usuario
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public string Email { get; set; }
}

public class UsuarioDto
{
    public int Id { get; set; }
    public string NombreCompleto { get; set; }
    public string CorreoElectronico { get; set; }
}


2. Método de Mapeo Manual
Podemos implementar un método que realice el mapeo manualmente:

csharp
Copiar código
public UsuarioDto MapearAUsuarioDto(Usuario usuario)
{
    return new UsuarioDto
    {
        Id = usuario.Id,
        NombreCompleto = usuario.Nombre,
        CorreoElectronico = usuario.Email
    };
}
Ejemplo de Uso de AutoMapper
1. Instalación
Para simplificar el proceso de mapeo, podemos utilizar una biblioteca como AutoMapper. Para instalar AutoMapper, puedes usar NuGet:

bash
Copiar código
Install-Package AutoMapper
2. Configuración
Primero, configuramos AutoMapper:

csharp
Copiar código
var config = new MapperConfiguration(cfg =>
{
    cfg.CreateMap<Usuario, UsuarioDto>()
        .ForMember(dest => dest.NombreCompleto, opt => opt.MapFrom(src => src.Nombre))
        .ForMember(dest => dest.CorreoElectronico, opt => opt.MapFrom(src => src.Email));
});

IMapper mapper = config.CreateMapper();
3. Uso de AutoMapper
Luego, podemos usar AutoMapper para realizar el mapeo:

csharp
Copiar código
Usuario usuario = new Usuario { Id = 1, Nombre = "Lucas", Email = "lucas@example.com" };
UsuarioDto usuarioDto = mapper.Map<UsuarioDto>(usuario);
Ventajas del Mapeo
Simplificación: Reduce la cantidad de código repetitivo al mapear entre diferentes tipos de objetos.
Flexibilidad: Permite realizar modificaciones en el mapeo de manera centralizada, lo que facilita los cambios en el modelo de datos.
Integración con Frameworks: Herramientas como AutoMapper se integran fácilmente con otros frameworks y tecnologías, mejorando la productividad del desarrollador.
Desventajas del Mapeo
Desempeño: Dependiendo de la complejidad de los objetos y el tamaño de los datos, el mapeo puede tener un impacto en el rendimiento.
Configuración Adicional: La utilización de herramientas de mapeo como AutoMapper puede requerir tiempo adicional para su configuración y aprendizaje.
