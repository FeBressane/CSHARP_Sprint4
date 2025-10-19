# 🧩 Sprint4.CSharp.WebApi (ASP.NET Core + EF Core + Swagger)

## Alunos
- Camila do Prado Padalino – RM98316
- Felipe Cavalcante Bressane – RM97688 
- Gabriel Teixeira Machado – RM551570 
- Guilherme Brazioli – RM98237

## Entrega da **Sprint 4 – C#** com os itens do enunciado
- **ASP.NET Core Web API + Entity Framework Core com CRUD completo**  
  - `ProductsController` com **Create / Read / Update / Delete** e relacionamento `Product → Category`.  
  - Banco **SQLite** criado automaticamente com *seed* inicial.
- **Pesquisas com LINQ**  
  - `LinqController` com **busca por nome**, **Top N por preço** e **paginação**.
- **Documentação do projeto**  
  - **Swagger** habilitado na raiz da aplicação + comentários XML.  
  - **README** (este arquivo) e coleção **Postman** para testes.
- **Arquitetura em diagramas**  
  - Diagrama em **Mermaid** (`/Diagrams/arquitetura.md`).

> ❌ *Escopo desta versão (v2):* **sem publicação em Cloud** e **sem integração com API externa**, conforme a imagem do enunciado enviado.

---

## Como rodar
1. **Pré-requisitos:** `dotnet 8 SDK`.  
2. Abra a pasta do projeto `Sprint4.CSharp.WebApi`.  
3. Restaure e compile:
   ```bash
   dotnet restore
   dotnet build
   ```
4. Execute:
   ```bash
   dotnet run
   ```
5. Acesse o **Swagger** na raiz (ex.: `http://localhost:5000` ou `https://localhost:5001`).  
   > O arquivo **SQLite** `app.db` é criado automaticamente no primeiro run.

---

## Uso rápido (via Swagger)
1. Abra o **Swagger UI**.  
2. Em **/api/products**:
   - `POST` para criar um produto (use uma `CategoryId` existente).  
   - `GET` para listar, `GET {id}` para detalhes, `PUT {id}` para atualizar e `DELETE {id}` para remover.
3. Em **/api/linq**:
   - `GET /search?term=mouse` → busca por nome.  
   - `GET /top-expensive?take=3` → Top N por preço.  
   - `GET /paged?page=1&pageSize=2` → paginação simples.

---

## Camadas & Responsabilidades
- **Models**: entidades `Product` e `Category`.  
- **Data**: `AppDbContext` (EF Core) + `Seed` de dados.  
- **Repositories**: `EfRepository<T>` (exemplo de repositório genérico).  
- **Controllers**:  
  - `ProductsController` (CRUD completo).  
  - `LinqController` (consultas LINQ).  
- **Docs/Diagrams**: documentação e diagrama de arquitetura (Mermaid).

---

## Estrutura de Pastas
```
Sprint4.CSharp.WebApi/
  Controllers/
    LinqController.cs
    ProductsController.cs
  Data/
    AppDbContext.cs
  DTOs/
    ProductCreateDto.cs
    ProductReadDto.cs
  Models/
    Category.cs
    Product.cs
  Repositories/
    EfRepository.cs
    IRepository.cs
  Diagrams/
    arquitetura.md
  Postman/
    Sprint4_CSharp_Revisado.postman_collection.json
  Program.cs
  appsettings.json
  Sprint4.CSharp.WebApi.csproj
```

---

## Endpoints principais

### Produtos (CRUD)
- `GET /api/products` – lista todos (com `CategoryName`)  
- `GET /api/products/{id}` – obtém por ID  
- `POST /api/products` – cria (body: `ProductCreateDto`)  
- `PUT /api/products/{id}` – atualiza  
- `DELETE /api/products/{id}` – remove

### LINQ
- `GET /api/linq/search?term={texto}` – busca *contains* (case-insensitive)  
- `GET /api/linq/top-expensive?take=3` – Top N por preço (desc)  
- `GET /api/linq/paged?page=1&pageSize=2` – paginação simples
