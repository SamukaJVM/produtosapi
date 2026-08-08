# Primeiros Passos com Spring Boot

Este módulo apresenta os primeiros passos no desenvolvimento de aplicações utilizando **Spring Boot**, desde a criação e configuração do projeto até a implementação de uma API com operações de **CRUD**, integração com banco de dados e utilização do **JPA/Hibernate**.

---

## 📚 Conteúdo

### 1. Criando um projeto Spring Boot

Introdução à criação de um projeto utilizando Spring Boot.

* Criação de um projeto Spring Boot
* Configuração inicial da aplicação
* Escolha das dependências
* Estrutura básica do projeto
* Organização dos pacotes
* Execução da aplicação

Estrutura inicial:

```text
projeto
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
├── pom.xml
└── ...
```

---

### 2. Conhecendo a estrutura do projeto e dicas Maven

Entendimento dos principais arquivos e diretórios de um projeto Spring Boot.

```text
src/main/java
    └── Código-fonte da aplicação

src/main/resources
    ├── application.properties
    └── Scripts e recursos

src/test
    └── Testes automatizados

pom.xml
    └── Configuração e dependências Maven
```

### Maven

Introdução aos principais conceitos do Maven:

* `pom.xml`
* Dependências
* Plugins
* Lifecycle
* Build do projeto
* Gerenciamento de versões
* Diretório `target`

---

### 3. Hello World com Spring Boot

Criação da primeira funcionalidade utilizando Spring Boot.

Exemplo de um endpoint:

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello World!";
    }
}
```

Fluxo:

```text
Cliente
   │
   │ GET /hello
   ▼
Controller
   │
   ▼
"Hello World!"
```

O objetivo é compreender o funcionamento básico de uma aplicação web utilizando Spring Boot.

---

# 🌐 API e Operações com Produtos

### 4. Criando endpoint para recebimento dos produtos

Criação de um endpoint responsável por receber informações de produtos através de requisições HTTP.

Exemplo:

```http
POST /produtos
```

Dados enviados:

```json
{
  "nome": "Notebook",
  "preco": 3500.00
}
```

Conceitos envolvidos:

* HTTP
* Endpoints
* `@RestController`
* `@PostMapping`
* JSON
* Requisição e resposta
* `@RequestBody`

---

# 🗄️ Banco de Dados

### 5. Configurando a conexão com o banco de dados

Configuração da aplicação Spring Boot para conexão com um banco de dados.

Exemplo de configuração:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/produtos
spring.datasource.username=root
spring.datasource.password=senha
```

Conceitos abordados:

* Datasource
* JDBC
* Driver do banco
* URL de conexão
* Usuário e senha
* Configuração através do `application.properties`

Fluxo:

```text
Spring Boot
     │
     ▼
DataSource
     │
     ▼
JDBC Driver
     │
     ▼
Banco de Dados
```

---

### 6. Executando SQL ao subir a aplicação Spring

Execução de scripts SQL durante a inicialização da aplicação.

Possibilidade de utilizar arquivos como:

```text
src/main/resources/
└── schema.sql
```

Exemplo:

```sql
CREATE TABLE produto (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(255),
    preco DECIMAL(10,2)
);
```

Essa etapa permite preparar a estrutura inicial do banco automaticamente durante a execução da aplicação.

---

# 🧩 JPA e Persistência

### 7. Criando o mapeamento JPA para a entidade `Produto`

Criação da entidade Java responsável por representar o produto no banco de dados.

Exemplo:

```java
@Entity
public class Produto {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String nome;

    private BigDecimal preco;
}
```

Conceitos:

* JPA
* Hibernate
* `@Entity`
* `@Id`
* `@GeneratedValue`
* Mapeamento objeto-relacional
* Entidade × tabela
* Atributo × coluna

Representação:

```text
Java                         Banco
─────────────────────────────────────
Produto       ───────────►  produto
id            ───────────►  id
nome          ───────────►  nome
preco         ───────────►  preco
```

---

### 8. Persistindo produtos no banco de dados

Implementação da persistência dos produtos utilizando JPA.

Exemplo de Repository:

```java
public interface ProdutoRepository
        extends JpaRepository<Produto, Long> {
}
```

Fluxo:

```text
POST /produtos
      │
      ▼
Controller
      │
      ▼
Service
      │
      ▼
Repository
      │
      ▼
JPA / Hibernate
      │
      ▼
Database
```

O Spring Data JPA simplifica diversas operações de persistência.

---

# 🔄 Operações CRUD

### 9. Obtendo os dados do produto

Implementação de consultas para recuperar produtos.

Exemplos:

```http
GET /produtos
```

ou:

```http
GET /produtos/1
```

Conceitos:

* `@GetMapping`
* Busca por ID
* Lista de produtos
* `JpaRepository`
* Respostas HTTP

---

### 10. Deletando produtos

Implementação da remoção de produtos.

Exemplo:

```http
DELETE /produtos/1
```

Fluxo:

```text
DELETE Request
      │
      ▼
Controller
      │
      ▼
Repository
      │
      ▼
Database
```

---

### 11. Atualizando os dados de um produto

Implementação da alteração de produtos existentes.

Exemplo:

```http
PUT /produtos/1
```

Dados:

```json
{
  "nome": "Notebook Gamer",
  "preco": 4500.00
}
```

Fluxo:

```text
PUT
 │
 ▼
Controller
 │
 ▼
Service
 │
 ▼
Repository
 │
 ▼
Database
```

---

### 12. Realizando busca com parâmetros

Implementação de consultas utilizando parâmetros na requisição.

Exemplo:

```http
GET /produtos?nome=Notebook
```

Ou:

```http
GET /produtos?preco=3500
```

Conceitos:

* Query Parameters
* `@RequestParam`
* Filtros
* Consultas personalizadas
* Spring Data JPA

---

# 🏗️ Fluxo Completo da Aplicação

Ao final do módulo, teremos uma aplicação capaz de realizar operações básicas sobre produtos.

```text
                    Cliente
                       │
                       │ HTTP
                       ▼
                ┌─────────────┐
                │ Controller  │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │   Service   │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │ Repository  │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │ JPA/Hibernate│
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │  Database   │
                └─────────────┘
```

### Operações implementadas

| Operação  | HTTP     | Exemplo       |
| --------- | -------- | ------------- |
| Criar     | `POST`   | `/produtos`   |
| Listar    | `GET`    | `/produtos`   |
| Buscar    | `GET`    | `/produtos/1` |
| Atualizar | `PUT`    | `/produtos/1` |
| Deletar   | `DELETE` | `/produtos/1` |

---

# 🧪 Testando a API

As operações podem ser testadas utilizando ferramentas como **Postman**.

Exemplo:

```text
POST    /produtos
GET     /produtos
GET     /produtos/{id}
PUT     /produtos/{id}
DELETE  /produtos/{id}
```

Fluxo de teste:

```text
Postman
   │
   ▼
Spring Boot
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
Banco de Dados
```

---

# 🎯 Objetivo do Módulo

Ao concluir este módulo, você deverá ser capaz de:

* Criar um projeto Spring Boot
* Compreender a estrutura básica de um projeto
* Trabalhar com Maven
* Criar endpoints REST
* Receber e enviar dados em JSON
* Configurar uma conexão com banco de dados
* Executar scripts SQL
* Criar entidades JPA
* Utilizar Spring Data JPA
* Persistir dados
* Consultar registros
* Atualizar registros
* Excluir registros
* Trabalhar com parâmetros de requisição
* Implementar um CRUD básico

---

# 📝 Resumo

Neste módulo foram construídos os fundamentos práticos para desenvolvimento de uma aplicação Spring Boot:

```text
Spring Boot
     │
     ├── Maven
     │
     ├── REST API
     │
     ├── Banco de Dados
     │
     ├── JPA / Hibernate
     │
     └── CRUD
          │
          ├── Create
          ├── Read
          ├── Update
          └── Delete
```

Esse conhecimento servirá como base para os próximos módulos, onde a aplicação poderá evoluir para uma arquitetura mais completa, com **Spring Data JPA avançado, validações, tratamento de erros, testes, boas práticas, segurança e recursos avançados de APIs REST**.
