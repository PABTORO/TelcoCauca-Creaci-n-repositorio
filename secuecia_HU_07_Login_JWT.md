### Diagrama de Secuencia: Login JWT
```mermaid
sequenceDiagram
    autonumber
    actor Cliente as Comprador / Agricultor
    participant Controller as AuthController
    participant Service as AuthService
    participant Repo as UsuarioRepository
    database DB as PostgreSQL

    Cliente->>Controller: POST /api/v1/auth/login (LoginRequestDTO)
    Controller->>Service: autenticarUsuario(dto)
    Service->>Repo: findByCorreo(correo)
    Repo->>DB: SELECT * FROM usuarios_productores WHERE correo = ?
    DB-->>Repo: Datos usuario / hash
    Repo-->>Service: Optional<Usuario>
    Service-->>Controller: JwtResponseDTO(token)
    Controller-->>Cliente: HTTP 200 OK (JWT)
```
