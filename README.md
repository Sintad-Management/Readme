# Prueba Técnica - Gestión de Entidades

## Introducción

Este proyecto consiste en un sistema integral de gestión de usuarios y otras entidades, diseñado con un enfoque en la seguridad, escalabilidad y usabilidad. Implementa un backend robusto basado en **Spring Boot** con autenticación JWT, y un frontend interactivo construido en **Angular**.

El objetivo principal es gestionar entidades mediante operaciones CRUD, asegurando la correcta separación de responsabilidades y un diseño limpio en ambas capas.

## Tecnologías Utilizadas

### Backend

* **Spring Boot:** Framework principal.
* **Hibernate:** Gestión ORM.
* **MySQL:** Base de datos relacional.
* **JWT:** Implementación de seguridad mediante autenticación basada en tokens.
* **Swagger:** Documentación interactiva para APIs.
* **JUnit y Mockito:** Pruebas unitarias.

### Frontend

* **Angular:** Framework de desarrollo del cliente.
* **Bootstrap 5.3.3:** Diseño responsivo y moderno.
* **SweetAlert2:** Notificaciones dinámicas y atractivas.
* **Angular HTTPClient:** Consumo eficiente de la API REST.

## Estructura del Proyecto

### Backend

1. **Arquitectura y Diseño**
   * Arquitectura basada en **DDD (Domain-Driven Design)**.
   * Separación en capas:
      * **Dominio**: Contiene las entidades y la lógica del negocio.
      * **Aplicación**: Define comandos y consultas para gestionar las operaciones.
      * **Infraestructura**: Persistencia y configuración del entorno.

2. **Endpoints Principales**
   * CRUD para usuarios y otras entidades.
   * Autenticación JWT para garantizar acceso seguro.

3. **Ejemplo de Swagger UI:**
   * Visualización de todos los endpoints con sus detalles.
   * Pruebas directas desde la interfaz.

4. **Ejemplo de respuesta de error:**
    ```json
    {
        "timestamp": "2025-01-16T12:34:56",
        "status": "CONFLICT",
        "message": "El recurso ya existe en al base de datos",
        "status": 409
    }
    ```
   * Respuesta consistente para errores como:
      * Entidad no encontrada.
      * Datos duplicados.
      * Errores internos del servidor.

### Frontend

1. **Organización Modular**
   * Módulos individuales para cada funcionalidad.
   * **Componentes principales:**
      * Formulario de login y registro.
      * Tablas y formularios dinámicos para gestionar entidades.
      * Panel de administración

2. **Validación y Seguridad**
   * Validación de formularios en tiempo real.
   * **Route Guards** que verifican autenticación y roles antes de acceder a ciertas rutas.

3. **Diseño Responsivo**
   * Uso combinado de Bootstrap para un diseño moderno y adaptado a dispositivos móviles.

4. **Ejemplo de alerta visual con SweetAlert2:**
   * Implementación de alertas dinámicas para acciones como guardar, eliminar o errores inesperados.

## Capturas del Backend

1. **Swagger UI:**
   *Vista general de la documentación generada automáticamente con Swagger.*
   ![Swagger UI](https://i.imgur.com/wUjI6yW.png)

   *Detalle de los endpoints disponibles en la API.*
   ![Swagger UI](https://i.imgur.com/w47wMjT.png)

   *Gestión de autenticación solicitando token para acceder a los endpoints.*
   ![Swagger UI](https://i.imgur.com/Slzb5NP.png)

   *Registro de usuarios para autenticación posterior. No se permiten correos duplicados en la base de datos.*
   ![Swagger UI](https://i.imgur.com/tzga55V.png)
   ![Swagger UI](https://i.imgur.com/XUm3Xaw.png)

   *Verificación del registro en la base de datos.*
   ![Swagger UI](https://i.imgur.com/YM3bV1O.png)

   *Autenticación de usuarios para obtener el token.*
   ![Swagger UI](https://i.imgur.com/B32ihh2.png)

   *Acceso a endpoints protegidos pasando el token en el encabezado.*
   ![Swagger UI](https://i.imgur.com/HpAyUaY.png)

2. **Interfaz UI:**
   *Vista de la interfaz de inicio de sesión.*
   ![Interfaz UI](https://i.imgur.com/iJTCcYL.png)

   *Vista de la interfaz de registro de usuario*
   ![Interfaz UI](https://i.imgur.com/GDHJ2kp.png)


    *Vista de la interfaz de registro de usuario con validaciones.*
    ![Interfaz UI](https://i.imgur.com/A7LkfGJ.png)

    *Una vez creado el usuario, se redirige a la página de inicio de sesión con un mensaje de éxito.*

    ![Interfaz UI](https://i.imgur.com/T1ZFEWK.png)

    
    *Advertencia mostrada si se ingresan credenciales incorrectas.*

    ![Interfaz UI](https://i.imgur.com/4pTUSOE.png)


    *Ingreso a la aplicación con un mensaje de éxito.*
    ![Interfaz UI](https://i.imgur.com/GkKW2bo.png)


    *Creación de una entidad en el formulario con validaciones.*

    ![Interfaz UI](https://i.imgur.com/B5BP1oZ.png)

    ![Interfaz UI](https://i.imgur.com/AtzGebm.png)
    ![Interfaz UI](https://i.imgur.com/XHnWNY7.png)

    *Verificación de la creación de la entidad en la base de datos.*
    ![Interfaz UI](https://i.imgur.com/hTw4CAd.png)

    *Advertencia mostrada al eliminar o editar una entidad.*
    ![Interfaz UI](https://i.imgur.com/jDNthFX.png)
    ![Interfaz UI](https://i.imgur.com/GkKW2bo.png)

    *Creación de múltiples entidades.*
    ![Interfaz UI](https://i.imgur.com/0LLSZjU.png)

    *Visualización del formulario para ver tipos de contribuyentes y documentos.*
    ![Interfaz UI](https://i.imgur.com/IxhfOSV.png)
    ![Interfaz UI](https://i.imgur.com/ekH3xlm.png)

## Manejo Global de Excepciones

El sistema implementa un manejo global de excepciones para asegurar que los errores sean gestionados de manera consistente y se proporcionen respuestas claras y útiles a los clientes de la API. A continuación se describen las excepciones personalizadas y el controlador global de excepciones utilizado en el proyecto.

### Excepciones Personalizadas

- **DuplicateEntryException**: Se lanza cuando se intenta crear una entrada que ya existe en la base de datos.
- **InternalServerErrorException**: Se lanza cuando ocurre un error interno en el servidor.
- **NotFoundException**: Se lanza cuando no se encuentra el recurso solicitado.
- **TipoContribuyenteDeletionException**: Se lanza cuando ocurre un error específico al intentar eliminar un tipo de contribuyente.

### Controlador Global de Excepciones

El controlador global de excepciones (`RestResponseEntityExceptionHandler`) maneja todas las excepciones lanzadas por el sistema y proporciona respuestas HTTP adecuadas. Este controlador extiende `ResponseEntityExceptionHandler` y anula métodos para manejar excepciones específicas.

#### Ejemplo de Configuración

```java
@RestControllerAdvice
public class RestResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {

    @ExceptionHandler(DuplicateEntryException.class)
    protected ResponseEntity<Object> handleDuplicateEntryException(DuplicateEntryException ex) {
        ApiError apiError = new ApiError(HttpStatus.CONFLICT, ex.getMessage(), ex);
        return buildResponseEntity(apiError);
    }

    @ExceptionHandler(NotFoundException.class)
    protected ResponseEntity<Object> handleNotFoundException(NotFoundException ex) {
        ApiError apiError = new ApiError(HttpStatus.NOT_FOUND, ex.getMessage(), ex);
        return buildResponseEntity(apiError);
    }

    @ExceptionHandler(InternalServerErrorException.class)
    protected ResponseEntity<Object> handleInternalServerErrorException(InternalServerErrorException ex) {
        ApiError apiError = new ApiError(HttpStatus.INTERNAL_SERVER_ERROR, ex.getMessage(), ex);
        return buildResponseEntity(apiError);
    }

    @ExceptionHandler(TipoContribuyenteDeletionException.class)
    protected ResponseEntity<Object> handleTipoContribuyenteDeletionException(TipoContribuyenteDeletionException ex) {
        ApiError apiError = new ApiError(HttpStatus.BAD_REQUEST, ex.getMessage(), ex);
        return buildResponseEntity(apiError);
    }

    private ResponseEntity<Object> buildResponseEntity(ApiError apiError) {
        return new ResponseEntity<>(apiError, apiError.getStatus());
    }
}
```
# Resultados Obtenidos

## Backend funcional


![Manejo de excepciones en el backend](https://i.imgur.com/GusH2CG.png)
![Manejo de excepciones en el backend](https://i.imgur.com/Td8565v.png)
![Manejo de excepciones en el backend](https://i.imgur.com/Dgonznp.png)
![Manejo de excepciones en el backend](https://i.imgur.com/lW5WjRS.png)


## Frontend interactivo

- **Interfaces limpias, responsivas y con validaciones.**

## Cobertura de pruebas

- **Servicios y Controladores probados con JUnit y Mockito.**
- **Interacción API probada con Postman.**

## Integración fluida

- **Backend y frontend sincronizados, con un manejo eficiente de autenticación y registro de usuario.**

# Conclusión

Este proyecto demuestra la integración exitosa de tecnologías modernas como Spring Boot, Angular y MySQL para desarrollar un sistema eficiente, seguro y visualmente atractivo. La correcta implementación de arquitecturas y buenas prácticas asegura que el proyecto es escalable y fácil de mantener.

## Enlaces del Proyecto

- **Repositorio Backend:** [sintad-management-prueba-sintad-backend](https://github.com/Sintad-Management/prueba-sintad-backend)
- **Repositorio Frontend:** [sintad-management-prueba-sintad-frontend](https://github.com/Sintad-Management/prueba-sintad-frontend)
- **Organización:** [Sintad Management](https://github.com/Sintad-Management)
