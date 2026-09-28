# AutoBots - Automanager

Microsserviço em Java com Spring Boot para o cadastro de clientes de lojas de manutenção veicular e venda de autopeças. O projeto é uma atividade prática (ATVI) e implementa o CRUD completo das entidades do cliente.

## Tecnologias

- Java 17
- Spring Boot 2.6.3 (Web, Data JPA)
- Banco de dados H2 (em memória)
- Lombok
- Maven (Maven Wrapper incluso)

## Entidades

| Entidade |
|---|---|
| `Cliente`|
| `Documento` |
| `Endereco` | 
| `Telefone` |

Um cliente tem vários documentos, um endereço e vários telefones.


## Como executar

Requisito: JDK 17 instalado. Não é preciso instalar Maven nem banco de dados.

1. Abra um terminal na pasta `automanager`.
2. Rode:

```bash
# Windows
.\mvnw.cmd spring-boot:run

# Linux / macOS
./mvnw spring-boot:run
```

A aplicação sobe em `http://localhost:8080`. Também é possível abrir a pasta `automanager` no VS Code ou no Eclipse e executar a classe `AutomanagerApplication`.

O banco H2 fica em memória, então os dados voltam ao estado inicial a cada reinicialização. Ao iniciar, a aplicação cadastra um cliente de exemplo (Dom Pedro) com telefone, endereço e documentos.

## Endpoints

| Método | Rota | Descrição |
|---|---|---|
| GET | `/{entidade}/{entidade}/{id}` | Busca por id |
| GET | `/{entidade}/{entidade}s` | Lista todos |
| POST | `/{entidade}/cadastro` | Cadastra |
| PUT | `/{entidade}/atualizar` | Atualiza (envia o `id` e os campos a mudar) |
| DELETE | `/{entidade}/excluir` | Exclui (envia o `id` no corpo) |

Onde `{entidade}` é `cliente`, `documento`, `endereco` ou `telefone`. A busca por id e a listagem têm nomes um pouco diferentes:

| Entidade | Busca por id | Listar todos |
|---|---|---|
| Cliente | `/cliente/cliente/{id}` | `/cliente/clientes` |
| Documento | `/documento/documento/{id}` | `/documento/documentos` |
| Endereço | `/endereco/endereco/{id}` | `/endereco/enderecos` |
| Telefone | `/telefone/telefone/{id}` | `/telefone/telefones` |

O nome da entidade se repete na busca por id porque o padrão da rota do `ClienteControle` original foi mantido nos demais controles.

### Exemplos

Cadastrar um telefone:

```http
POST /telefone/cadastro
Content-Type: application/json

{
  "ddd": "11",
  "numero": "999998888"
}
```

Atualizar só o número desse telefone:

```http
PUT /telefone/atualizar
Content-Type: application/json

{
  "id": 2,
  "numero": "988887777"
}
```

Excluir:

```http
DELETE /telefone/excluir
Content-Type: application/json

{
  "id": 2
}
```
