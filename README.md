# ? Microserviço de Pagamentos - AluraFood

API REST para gerenciamento de pagamentos usando Spring Boot, MySQL e Docker.

## ?? Tecnologias

- **Java 17** + Spring Boot 2.6.7
- **Spring Data JPA** + Hibernate
- **MySQL 8.0** + Flyway
- **ModelMapper** + Lombok
- **Docker** + Docker Compose
- **Maven**

## ? Executar o Projeto

### 1?? Configurar variáveis de ambiente

O gere o arquivo `.env` com as credenciais de desenvolvimento.

**Variáveis necessárias:**

```bash
# Database Configuration
MYSQL_ROOT_PASSWORD=sua_senha_root
MYSQL_DATABASE=alurafood-pagamento
MYSQL_USER=seu_usuario
MYSQL_PASSWORD=sua_senha
```

### 2?? Subir a aplicação

**Opção A - Tudo no Docker:**
```bash
docker-compose up -d
```

**Opção B - Apenas MySQL no Docker:**
```bash
docker-compose -f docker-compose.dev.yml up -d
```

### 3?? Acessar

- **API:** http://localhost:8080/pagamentos
- **MySQL:** localhost:3307

## ? Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/pagamentos` | Lista todos |
| GET | `/pagamentos/{id}` | Busca por ID |
| POST | `/pagamentos` | Cria novo |
| PUT | `/pagamentos/{id}` | Atualiza |
| DELETE | `/pagamentos/{id}` | Remove |

**Exemplo de POST:**
```json
{
  "valor": 100.50,
  "nome": "João Silva",
  "numero": "1234567890123456",
  "expiracao": "12/2025",
  "codigo": "123",
  "formaDePagamentoId": 1,
  "pedidoId": 1
}
```

## ? Comandos Úteis

```bash
# Parar containers
docker-compose down

# Limpar banco de dados
docker-compose down -v

# Rebuild
docker-compose up -d --build

# Ver logs
docker-compose logs -f pagamentos-app

# Acessar MySQL
docker exec -it mysql-pagamentos mysql -u pagamentos_user -p
```

## ?? Variáveis de Ambiente

A aplicação Spring Boot usa estas variáveis (configuradas automaticamente pelo Docker Compose):

| Variável | Descrição | Padrão |
|----------|-----------|--------|
| `SPRING_DATASOURCE_URL` | URL de conexão JDBC | `jdbc:mysql://localhost:3307/alurafood-pagamento` |
| `SPRING_DATASOURCE_USERNAME` | Usuário do MySQL | Lê de `MYSQL_USER` |
| `SPRING_DATASOURCE_PASSWORD` | Senha do MySQL | Lê de `MYSQL_PASSWORD` |

**Para desenvolvimento local (sem Docker):**
```bash
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3307/alurafood-pagamento
export SPRING_DATASOURCE_USERNAME=pagamentos_user
export SPRING_DATASOURCE_PASSWORD=pagamentos_pass_123
./mvnw spring-boot:run
```

## ? Segurança

? **Protegido:**
- `.env` no `.gitignore`

?? **Importante:** Leia o arquivo `SECURITY.md` antes de produção!

## ? Referências

- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa)
- [Flyway](https://flywaydb.org/)
- [Docker Compose](https://docs.docker.com/compose/)


