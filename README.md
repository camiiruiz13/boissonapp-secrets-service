# BoissonApp Secrets Service

Microservicio de gestión centralizada de secretos para el ecosistema **BoissonApp**, desarrollado con Python y FastAPI.

## Descripción general

**BoissonApp Secrets Service** tiene como objetivo proporcionar un mecanismo seguro y centralizado para consultar secretos almacenados en **AWS Secrets Manager**.

El servicio estará diseñado para exponer una API REST interna que podrá ser consumida por diferentes microservicios, independientemente del lenguaje de programación utilizado, como Python o Java.

Su propósito es evitar la duplicación de lógica de integración con AWS Secrets Manager, centralizar el manejo de credenciales y establecer estándares comunes de seguridad, configuración y tratamiento de errores.

> **Estado del proyecto:** En desarrollo inicial. La integración con AWS, los endpoints y los controles de seguridad todavía están pendientes de implementación.

## Tecnologías

- **Python 3.12:** lenguaje de programación principal.
- **FastAPI:** framework para desarrollar la API REST.
- **Boto3:** SDK de AWS para Python.
- **AWS Secrets Manager:** almacenamiento y administración de secretos.
- **LocalStack:** simulación de servicios AWS en el entorno local.
- **Pytest:** pruebas unitarias y de integración.

## Funcionalidades previstas

- Consultar secretos almacenados en AWS Secrets Manager.
- Permitir el desarrollo y las pruebas locales mediante LocalStack.
- Resolver alias de secretos mediante una configuración centralizada.
- Proporcionar una API REST interna reutilizable por diferentes microservicios.
- Implementar autenticación y autorización entre servicios.
- Centralizar el manejo de errores y los registros de ejecución.
- Evitar la exposición de información sensible en los logs.
- Administrar la configuración según el entorno de ejecución.

## Arquitectura propuesta

```text
                 Ecosistema BoissonApp
                          |
             +------------+------------+
             |                         |
      Geography Service         Inventory Service
          (Python)                   (Java)
             |                         |
             +------------+------------+
                          |
                          v
              BoissonApp Secrets Service
                     (FastAPI)
                          |
                          v
                  AWS Secrets Manager
                          |
                   LocalStack / AWS
```

## API REST propuesta

Se contempla implementar el siguiente endpoint interno:

**GET /boissonapp/secrets/{alias}**

El parámetro `alias` identificará el secreto solicitado. El servicio resolverá internamente su nombre real en AWS Secrets Manager y verificará que el consumidor tenga autorización para consultarlo.

Ejemplo:

```text
Alias solicitado:
countrystatecity

Nombre del secreto en AWS:
boissonapp/dev/geography/countrystatecity
```

**Importante:** este endpoint todavía no está implementado y no deberá exponerse públicamente sin controles de autenticación y autorización.

## Seguridad

El proyecto seguirá los siguientes principios:

- No almacenar credenciales directamente en el código fuente.
- No publicar archivos `.env` con información sensible.
- No registrar valores de secretos en los logs.
- Restringir el acceso a los microservicios autorizados.
- Utilizar conexiones seguras entre servicios.
- Aplicar el principio de mínimo privilegio.
- Mantener los secretos fuera de las aplicaciones frontend, como Angular.

## Plan de desarrollo

- [x] Crear el proyecto Python con FastAPI.
- [x] Inicializar el repositorio Git.
- [ ] Configurar las dependencias del proyecto.
- [ ] Implementar la integración con AWS Secrets Manager.
- [ ] Configurar los entornos de ejecución.
- [ ] Implementar la resolución de alias.
- [ ] Desarrollar los endpoints REST.
- [ ] Implementar autenticación y autorización.
- [ ] Desarrollar pruebas unitarias y de integración.
- [ ] Integrar Docker y LocalStack.
- [ ] Configurar integración y despliegue continuos (CI/CD).
- [ ] Desplegar el servicio en AWS.

## Organización del proyecto

El microservicio seguirá una arquitectura por capas, separando las responsabilidades de configuración, dominio, integración con servicios externos y exposición de endpoints REST.

La estructura definitiva se establecerá conforme avance la implementación.

## Licencia

Proyecto privado desarrollado para el ecosistema BoissonApp.
