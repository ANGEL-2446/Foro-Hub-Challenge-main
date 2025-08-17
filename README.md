# 🧠 ForoHub API

API RESTful desarrollada con Spring Boot 3 para la gestión segura y documentada de tópicos de foro técnico. Incluye autenticación JWT, control granular de acceso por roles y documentación interactiva con Swagger UI. Ideal para entornos empresariales y educativos donde la seguridad y claridad son prioridad.

**Autor:** Ángel Alfonso Fernández Collao

---

## 🔐 Autenticación y Seguridad con JWT

El sistema implementa un flujo completo de autenticación basado en JSON Web Tokens (JWT), garantizando el acceso controlado a los recursos del backend:

### 🔄 Flujo de Autenticación

1. **Login de usuario (POST /auth/login):** El usuario envía credenciales válidas (email y contraseña).  
2. **Generación de Token JWT:** Si las credenciales son correctas, se devuelve un token firmado.  
3. **Acceso a recursos protegidos:** El token debe incluirse en cada solicitud como header \`Authorization: Bearer <token>\`.  
4. **Control por rol:** Algunos endpoints requieren roles específicos para operar (\`admin\`, \`usuario\`).  

### 🔍 Validaciones automáticas

- Tokens expirados o malformados generan error \`401 Unauthorized\`.  
- Acceso sin permisos suficientes responde con \`403 Forbidden\`.  
- Tokens válidos permiten acceso a operaciones como crear, listar y responder tópicos.

---

## 📘 Documentación Interactiva con Swagger UI

Se incluyó Swagger/OpenAPI v3 para generar documentación técnica y habilitar pruebas interactivas desde el navegador:

- **Acceso:** \`/swagger-ui/index.html\`  
- Soporta login directo desde Swagger  
- Permite probar recursos protegidos usando el token JWT  
- Muestra modelos de datos, parámetros requeridos y ejemplos de respuesta  

La seguridad está definida a nivel global en Swagger, lo que permite usar **Authorize** una sola vez para todos los endpoints protegidos.

---

## 🧩 Endpoints disponibles

| Endpoint             | Método | Seguridad | Descripción                          |
|---------------------|--------|-----------|--------------------------------------|
| `/auth/login`        | POST   | Público   | Autenticación del usuario            |
| `/topicos`           | GET    | Protegido | Listado de tópicos del foro          |
| `/topicos`           | POST   | Protegido | Crear nuevo tópico                    |
| `/respuestas/{id}`   | POST   | Protegido | Responder a un tópico específico     |

> Todos los endpoints protegidos requieren JWT válido y perfil autorizado.

---

## 🧪 Pruebas recomendadas

Para garantizar la seguridad y robustez, se recomienda realizar las siguientes pruebas:

- ✅ Login exitoso con credenciales válidas  
- 🚫 Acceso denegado sin token o con token inválido  
- 🔄 Token expirado y comportamiento frente al refresh  
- 🧾 Validación de roles accediendo a recursos restringidos  
- 🐞 Pruebas desde Swagger UI simulando usuarios reales  

---

## 📦 Tecnologías utilizadas

- Java 17 + Spring Boot 3  
- Spring Security + JWT  
- JPA + Hibernate  
- Flyway para control de migraciones SQL  
- Swagger/OpenAPI para documentación técnica  
- Maven como gestor de dependencias  

---

## 🗄️ Base de Datos

La API utiliza **MySQL** como sistema de almacenamiento relacional. Se eligió por su robustez, compatibilidad con JPA/Hibernate y facilidad de integración con Spring Boot.

**Características clave:**

- ✅ Motor: MySQL Server  
- 🗂️ Persistencia gestionada con JPA/Hibernate  
- 🚀 Migraciones controladas con Flyway (\`src/main/resources/db/migration\`)  
- 🔐 Integridad referencial y validación por esquema SQL  
- ⚙️ Conexión configurada vía \`application.properties\`  
